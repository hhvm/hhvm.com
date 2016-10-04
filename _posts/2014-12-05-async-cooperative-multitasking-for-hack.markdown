---
author: sgolemon
comments: true
layout: post
title: Async - Cooperative Multitasking for Hack
category: blog
permalink: /blog/7091/async-cooperative-multitasking-for-hack
---

For several months now, Hack has had a feature available called `async` which enables writing code that cooperatively multitasks. This is somewhat similar to threading, in that multiple code paths are executed in parallel, however it avoids the lock contention issues common to multithreaded code by only actually executing one section at any given moment.

<!--truncate-->

"What's the use of that?", I hear you ask.  You're still bound to one CPU, so it should take the same amount of time to execute your code, right?  Well, that's technically true, but script code execution isn't the only thing causing latency in your application.  The biggest piece of it probably comes from waiting for backend databases to respond to queries.

When you call `$zuck = file_get_contents('https://graph.facebook.com/4');`, the runtime essentially pauses execution while it waits for network packets to cross the internet, query a database for an answer, and come back.  About 350ms from my house, more than 200 of which is just to negotiate TLS. 350ms is practically an eternity on the scale of a web request.

That's where cooperative multitasking comes in.  While your https call is busy sitting on its hands waiting for a response, there's no reason you shouldn't be able to do other things, maybe even fire off more requests.  The same goes for database queries, which can take just as long, or even filesystem access which is faster than network, but can still introduce lag times of several milliseconds, and those all add up!

So how do we write code that can cooperate with other code?  Hack's solution for that, as I said earlier, is `async`, and its sibling structures `await`, `WaitHandle`, and `Awaitable`.  Let's take a look at a simplified example; a single task which can run in all the glorious parallelism of lone execution.


```php
<?hh

async function hello(): Awaitable<string> {
  return "Hello World";
}

$a = hello();
var_dump($a);
var_dump($a->getWaitHandle()->join());

// Object(HH\StaticWaitHandle)#1 (0) {
// }
// string(11) "Hello World"
```


Immediately of notice is that returning from a function (or method) marked as "`async`" doesn't actually return that value, it returns a instance of a WaitHandle object (in this case, an `HH\StaticWaitHandle`, but we'll see other types).  We don't see the actual value until, as the caller, we've told the underlying async layer "wait until this task has done all its work, then give me the value".  This is because, like a generator, the async function is designed to be pauseable and resume execution at a later time.

Most places in an async code base, that will be done by invoking `$result = await $waitHandle;` because that leaves the CPU free to run through other async functions`, however at the top-most point, where there's nothing else to share processing time with, we use a hard-block in the form of `$handle->join();`  Which effectively says "Deal with all your pending handles, then give me the end result."  Let's try adding a line to this function:


```php
<?hh

async function hello(): Awaitable<string> {
  await RescheduleWaitHandle::create(
    RescheduleWaitHandle::QUEUE_DEFAULT,
    0,
  );
  return "Hello World";
}
```


This function produces the same results, but this time we've used `RescheduleWaitHandle` to say "If there's any other async function trying to run right now, let it have some fun, come back to me when you've got nothing better to do." Again, because we're inside of an async function, we use `await`, rather than `join()`, because we're probably sharing the stage with some other async function somewhere else, so we don't want the hard block which comes from `join()`.  Similarly, we could schedule a sleep to wait an arbitrary amount of time:


```php
<?hh

async function hello(): Awaitable<string> {
  await SleepWaitHandle::create(1000); /* 1000us, aka 1ms */
  return "Hello World";
}
```


But those uses are all pretty silly, especially considering that we only have one task to perform which will ultimately have to block on the ->join() call anyway. How can we do more than one thing? Enter `AwaitAllWaitHandle` which organizes execution of an arbitrary number of WaitHandles passed to it as an array, Map, or Vector.

```php
<?hh

async function hello(): Awaitable<string> {
  return "Hello World";
}
async function goodbye(): Awaitable<string> {
  return "Goodbye, everybody!";
}
async function run(
  array<WaitHandle<string>> $handles,
): Awaitable<array<string>> {
  await AwaitAllWaitHandle::fromArray($handles);
  return array_map($handle ==> $handle->result(), $handles);
}
$results = run(array(hello(), goodbye()))->getWaitHandle()->join();
print_r($results);
// Array
// (
//  [0] => Hello World
//  [1] => Goodbye, everybody!
// )
```


`AwaitAllWaitHande::fromArray()` (and its Collection cousins `AwaitAllWaitHandle::fromVector()` and `AwaitAllWaitHandle::fromMap()`) don't actually yield values, instead they queue execution of their children such that when the `AwaitAllWaitHandle` yields, all of its handles will be done (as we could test with `->isFinished()`).  Subsequent calls to `->result()` will return each handle's value, just as if we had called `->join()`.

So that's great and all, but none of this is blocking code, and we still haven't seen an advantage over just executing them in series. In fact, they are effectively executed in series because it's just cooperative multitasking, not multi-threading. So let's add in the simplest kind of blocking call, an http fetch using cURL. The work-horse of this feature is the following builtin function:


```php
async function curl_multi_await(
  resource $curlMultiHandle,
  float $timeout = 1.0,
): Awaitable<int>;
```


This allows us to "await" on the only part of a curl request which actually needs to block. It's a bit unhelpful all by itself, so let's make a simple wrapper for it:


```php
<?hh
async function curl_exec_await(string $url): Awaitable<string> {
  $ch = curl_init($url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

  $mh = curl_multi_init();
  curl_multi_add_handle($mh, $ch);
  do {
    $active = 1;
    do {
      $status = curl_multi_exec($mh, $active);
    } while ($status == CURLM_CALL_MULTI_PERFORM);
    $select = await curl_multi_await($mh);
    if ($select == -1) break;
  } while ($status === CURLM_OK);
  $content = (string)curl_multi_getcontent($ch);
  curl_multi_remove_handle($mh, $ch);
  curl_multi_close($mh);
  return $content;
}
```


During lulls in network activity, the `await curl_multi_async($mh);` allows us to pass control to another `WaitHandle` (perhaps another curl request, perhaps something else), meanwhile the rest of the execution performs non-blocking actions, like calling `curl_multi_exec()`. Armed with this helper, and our lessons from earlier, we can combine this all into multiple parallelized fetches:


```php
<?hh
include "curl-exec-await.php";

$results = run(array(
  curl_exec_await("https://graph.facebook.com/4"),
  curl_exec_await("http://www.example.om"),
  curl_exec_await("http://www.hhvm.com"),
))->getWaitHandle()->join();
```


If you're still paying attention, then you're probably wondering why we couldn't just pass multiple easy handles into one multi handle and use the curl-multi interface that PHP's known and loved for years. And you'd be right to wonder. If the only operation we were performing were cURL calls, then we could certainly get by with the existing curl-multi interface. Where async really starts to shine is when you combine other awaitable resources into the picture. Imagine something like this:


```php
<?hh

async function fibonacci_gen(int $num): int {
  $n1 = 0; $n2 = 1; $n3 = 1;
  for ($i = 2; $i < $num; ++$i) {
    $n3 = $n1 + $n2;
    $n1 = $n2;
    $n2 = $n3;
    if (!($i % 100)) {
      // Give other tasks a chance to do something
      // every 100th iteration
      await RescheduleWaitHandle::create(
        RescheduleWaitHandle::QUEUE_DEFAULT,
        0,
      );
    }
  }
  return $n3;
}
$results = run(array(
  "web"  => curl_exec_await("http://example.com"),
  "sql"  => mysql_async_query($conn, "SELECT * FROM user"),
  "disk" => file_async_contents("/var/log/access.log"),
  "mc"   => memcached_async_get("somekey"),
  "fib"  => fibonacci_gen(2000),
))->getWaitHandle()->join();
```


Now we're combining multiple kinds of blocking operations (and one expensive bit of pure script code) in a single coordination framework without having to know, from the callsite, how to block on the underlying file descriptors or when.

For now, there's no streams, mysql, or memcached APIs for async blocking, but streams should arrive soon (it's currently up for review), and memcached/webscalesql support are hot on its heels. Watch this space for those.

> As you can see from the paragraph above, async is still in active development, so you'll need HHVM 3.5.0 (which may not exist at the time of this reading) or a nightly to get the curl support.  Check out [installing nightlies on Ubuntu](https://github.com/facebook/hhvm/wiki/Prebuilt-packages-on-Ubuntu-14.10) or elsewhere in the HHVM wiki for more info on how to do that.
