---
author: sgolemon
layout: post
title: Async - Cooperative Multitasking for Hack
category: blog
permalink: /blog/7091/async-cooperative-multitasking-for-hack
comments:
- id: 309329
  author: Carl G
  date: '2014-12-05 10:50:15 +0000'
  date_gmt: '2014-12-05 18:50:15 +0000'
  content: "This is cool. But, going a little off-topic, I'm really starting to wonder
    why you've even released Hack to the public.\r\n\r\nI'm a professional, and using
    a new language puts a dent in my productivity for a while.\r\n\r\nGoing backwards
    from an advanced IDE like phpStorm to a text editor and package of CLI tools is
    another huge productivity hit.\r\n\r\nThose combined mean I'll never be able to
    adopt Hack unless you get us some IDE support.\r\n\r\nI know most other devs are
    in the same boat. You're basically talking to yourselves until you release FBIDE
    or a plugin for phpStorm, Netbeans, or some other PHP-loving IDE.\r\n\r\nThese
    new features are nice, but maybe you could hit the breaks for a (few?) weeks and
    just get the IDE out."
- id: 309359
  author: Vincent DM
  date: '2014-12-05 11:16:54 +0000'
  date_gmt: '2014-12-05 19:16:54 +0000'
  content: "@Carl G: I can only agree! I don't want to whine, and I sincerely appreciate
    all the time and effort Facebook and its people are investing into hack, but it's
    almost tragic how the language is closely watched by many but used by relatively
    few. Proper IDE support is a vital step to kickstart the community, I think. Until
    then, I'm sticking with PHP and some nodejs for async stuff..."
- id: 309371
  author: Sara Golemon
  date: '2014-12-05 11:40:29 +0000'
  date_gmt: '2014-12-05 19:40:29 +0000'
  content: "AIUI, several editor projects and their communities are working on hack
    plugins.  IMO these should be in the hands of developers who actually use these
    tools as they're the best ones for that task.\r\n\r\nAs for FBIDE... yeah... I
    wish the team responsible for that would get on releasing it too..."
- id: 309611
  author: Paul Moss
  date: '2014-12-05 18:38:38 +0000'
  date_gmt: '2014-12-06 02:38:38 +0000'
  content: "So when it the memcached&#47;webscale support due, for 3.5 or 3.6?\r\n\r\nWould
    this also include memcached which comes with mysql 5.6?\r\n\r\nFinally, does webscale
    mean mysql 5.6 client as well?\r\n\r\nEssentially, I would love to parallelise
    my requests for memcached and mysql.  Can't wait really."
- id: 309989
  author: Jeroen De Dauw
  date: '2014-12-06 03:54:42 +0000'
  date_gmt: '2014-12-06 11:54:42 +0000'
  content: Another +1 to this. I've been wanting to do some katas in Hack for months
    now, yet can't bring myself to start without proper IDE support. I want to take
    a step forewards without taking one or two backwards first.
- id: 309995
  author: ip512
  date: '2014-12-06 04:08:48 +0000'
  date_gmt: '2014-12-06 12:08:48 +0000'
  content: "Guzzle has already asynchonous response management (http:&#47;&#47;guzzle.readthedocs.org&#47;en&#47;latest&#47;clients.html#asynchronous-response-handling)\r\nIn
    which case this asynchronous approach can be preferable over using Guzzle ?"
- id: 310535
  author: Brice
  date: '2014-12-06 15:56:23 +0000'
  date_gmt: '2014-12-06 23:56:23 +0000'
  content: "Yes, it would be great to have validation and syntax highlighting working
    in eclipse with vi + emacs as well.\r\n\r\nIMO -- Eclipse support is the priority
    as it's the official base of PDT. The commerical projects like intellij, storm,
    &amp;c could base their support from there.\r\n\r\nTotally excited about hack
    &amp; hvvm in general! Keep it up."
- id: 310673
  author: Sara Golemon
  date: '2014-12-06 23:05:20 +0000'
  date_gmt: '2014-12-07 07:05:20 +0000'
  content: "memcached looks like it'll be relatively soon, though I can't guarantee
    it'll be in by 3.5.  We'll be using mcrouter as the underlying client library
    (as libmemcached doesn't have a good async interface), but it should work against
    anything that supports the memcached protocol...\r\n\r\n\"webscale\" means the
    async support will require libwebscalesqlclient on the *client* side.  The actual
    server can be WebscaleSQL, MySQL, MariaDB, or anything which speaks the mysql
    protocol.\r\n\r\nI can't wait to round out the DB async support either!  Very
    exciting. :)"
- id: 310679
  author: Sara Golemon
  date: '2014-12-06 23:07:59 +0000'
  date_gmt: '2014-12-07 07:07:59 +0000'
  content: I don't know Guzzle well, but glancing through that link, it looks like
    it's only for http(s) requests.  Hack-Async covers that (via async-curl), but
    also includes many other types of blocking requests as well.  So personally, I
    would prefer using Hack-Async, but in the end you want to go for whatever makes
    sense for your application and your developer(s).
- id: 310943
  author: Asynchronous PHP ~ ma.ttias.be
  date: '2014-12-07 11:05:38 +0000'
  date_gmt: '2014-12-07 19:05:38 +0000'
  content: "[&#8230;] A really cool feature landed in HHVM, providing async PHP calls.
    [&#8230;]"
- id: 311981
  author: 'Hack Blog: Async &#8211; Cooperative Multitasking for Hack - Reader'
  date: '2014-12-08 12:00:12 +0000'
  date_gmt: '2014-12-08 20:00:12 +0000'
  content: "[&#8230;] the Hack blog there&#8217;s a new post talking about async,
    a feature in Hack that allows for code to &#8220;cooperatively multitask&#8221;.
    This gives the [&#8230;]"
- id: 312269
  author: Paul Moss
  date: '2014-12-08 18:21:44 +0000'
  date_gmt: '2014-12-09 02:21:44 +0000'
  content: "Sarah, thanks for the reply and the clarification!\r\n\r\nYou and the
    guys who work on this totally rock!\r\n\r\nYes, its very exciting, I can't wait!
    :)"
- id: 315737
  author: Fred Emmott
  date: '2014-12-12 15:07:46 +0000'
  date_gmt: '2014-12-12 23:07:46 +0000'
  content: "It would be possible to build this async approach into guzzle.\r\n\r\nAs
    well as async&#47;await giving a single approach to any kind of blocking request
    (which will become more useful as we release more), we generally feel that the
    async&#47;await flow is easier to work with than callbacks, which tend to lead
    to spaghetti code."
- id: 317447
  author: FractalizeR
  date: '2014-12-15 02:20:12 +0000'
  date_gmt: '2014-12-15 10:20:12 +0000'
  content: I wonder, how this will be transpiled into PHP? (https:&#47;&#47;code.facebook.com&#47;posts&#47;398235553660954&#47;announcing-the-hack-transpiler&#47;)
- id: 318749
  author: Jesse Cascio
  date: '2014-12-17 10:54:11 +0000'
  date_gmt: '2014-12-17 18:54:11 +0000'
  content: "NOOO!!! you took my blog post haha, I just did this on Dec 1 and it took
    me so long to figure out how to do it.  \r\n\r\nhttp:&#47;&#47;jessesnet.com&#47;development-notes&#47;2014&#47;hacklang-async-processing&#47;\r\n\r\nThanks
    for sharing, I'm going to go through this in more detail and see what I could
    have done better."
- id: 321539
  author: Stefan Parker
  date: '2014-12-21 14:11:45 +0000'
  date_gmt: '2014-12-21 22:11:45 +0000'
  content: I've been converting my project to use async in all the memcache-fetching
    (as in, combining memcache gets) code paths, and I've noticed anecdotally that
    the web request actually takes longer now. Because this is all locally my data-fetching
    is essentially 0ms, but is it true that execution time with an async structure
    is actually (noticeably) slower than without?
- id: 327683
  author: Vincent
  date: '2014-12-29 10:16:26 +0000'
  date_gmt: '2014-12-29 18:16:26 +0000'
  content: What was the reasoning behind this style of implementation for async, as
    opposed to the function callback style?
- id: 328877
  author: Jan Oravec
  date: '2014-12-30 16:22:52 +0000'
  date_gmt: '2014-12-31 00:22:52 +0000'
  content: async&#47;await makes it possible to structure asynchronous code in the
    same way as if it was implemented synchronously, resulting in significantly shorter
    and more readable code.
- id: 334151
  author: PHP Annotated Monthly &ndash; January 2015 | JetBrains PhpStorm Blog
  date: '2015-01-07 05:28:59 +0000'
  date_gmt: '2015-01-07 13:28:59 +0000'
  content: "[&#8230;] Golemon posted about cooperative multitasking in HHVM. Similar
    to threading, it allows multiple code paths to execute in parallel, yet only one
    section [&#8230;]"
- id: 338561
  author: 'Episode 34: &#47;dev&#47;hell Mashup | PHP Podcasts'
  date: '2015-01-14 00:43:33 +0000'
  date_gmt: '2015-01-14 08:43:33 +0000'
  content: "[&#8230;] Hack&rsquo;s Async stuff [&#8230;]"
- id: 339143
  author: Terry Cullen
  date: '2015-01-14 15:59:59 +0000'
  date_gmt: '2015-01-14 23:59:59 +0000'
  content: Is there a list somewhere of what works asynchronously and what doesn't?  Am
    I correct in thinking that all regular PHP can run async but code that calls extensions
    (like pdo, redis) needs the extension to be updated to run async?  What about
    the all the different wrappers in http:&#47;&#47;php.net&#47;manual&#47;en&#47;wrappers.php
    ?  Can things like file_get_contents() be called async?
- id: 349559
  author: Aftab Naveed
  date: '2015-01-26 16:33:31 +0000'
  date_gmt: '2015-01-27 00:33:31 +0000'
  content: if it still uses one CPU core to process the request,  my question is how
    come it passes control to next task when that core is still busy and waiting for
    the request to finish? is there any other example which can elaborate this ?
- id: 378839
  author: 'Episode 54: Phil is Still Wrong | PHP Podcasts'
  date: '2015-02-17 00:47:40 +0000'
  date_gmt: '2015-02-17 08:47:40 +0000'
  content: "[&#8230;] Hack&#8217;s Async stuff [&#8230;]"
- id: 439067
  author: Guilherme Cardoso
  date: '2015-04-03 21:30:14 +0000'
  date_gmt: '2015-04-04 04:30:14 +0000'
  content: Mongodb, that would be a great implementation!
- id: 480803
  author: Multitasking in Hack mit async-Feature - entwickler.de
  date: '2015-05-08 02:40:16 +0000'
  date_gmt: '2015-05-08 09:40:16 +0000'
  content: "[&#8230;] der Einsatz von async in der Praxis aussehen kann, beschreibt
    Sara Golemon ausf&uuml;hrlich und mit zahlreichen Code-Beispielen im HHVM-Blog.
    Derzeit befindet sich das Feature noch in der aktiven Entwicklung und soll mit
    HHVM [&#8230;]"
- id: 511709
  author: hhvm-rocks
  date: '2015-06-04 07:36:24 +0000'
  date_gmt: '2015-06-04 14:36:24 +0000'
  content: "...await curl_multi_async($mh); allows us to pass control to another...\r\n\r\njust
    a small correction; it should be \"await curl_multi_await($mh);\""
- id: 526655
  author: Aftab Naveed
  date: '2015-06-16 02:21:00 +0000'
  date_gmt: '2015-06-16 09:21:00 +0000'
  content: Sorry I wanted to clarify my question here as that sounds really stupid,
    comparing to Google Golang concurrency which uses the same core but switches control
    to another core if required, was wondering if HACK async does similar kind of
    thing?
- id: 526661
  author: Aftab Naveed
  date: '2015-06-16 02:22:27 +0000'
  date_gmt: '2015-06-16 09:22:27 +0000'
  content: Are there any async implementations planned for Guzzle?
- id: 528545
  author: Fred Emmott
  date: '2015-06-18 14:59:54 +0000'
  date_gmt: '2015-06-18 21:59:54 +0000'
  content: "That's really up to the Guzzle developers; we don't plan on creating a
    fork.\r\n\r\nWe do provide async curl and stream primitives."
- id: 762989
  author: HHVM Class Undefined SleepWaitHandle - HTML CODE
  date: '2016-01-16 02:42:34 +0000'
  date_gmt: '2016-01-16 10:42:34 +0000'
  content: "[&#8230;] i tried running demo http:&#47;&#47;hhvm.com&#47;blog&#47;7091&#47;async-cooperative-multitasking-for-hack
    [&#8230;]"
- id: 770531
  author: Fred Emmott
  date: '2016-01-21 11:23:19 +0000'
  date_gmt: '2016-01-21 19:23:19 +0000'
  content: 'This blog post is very old; the modern approach is documented here: https:&#47;&#47;docs.hhvm.com&#47;hack&#47;async&#47;utility-functions'
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

Most places in an async code base, that will be done by invoking `$result = await $waitHandle;` because that leaves the CPU free to run through other async functions, however at the top-most point, where there's nothing else to share processing time with, we use a hard-block in the form of `$handle->join();`  Which effectively says "Deal with all your pending handles, then give me the end result."  Let's try adding a line to this function:


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
