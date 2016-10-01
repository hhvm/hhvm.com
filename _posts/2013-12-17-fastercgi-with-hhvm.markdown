---
author: julk
comments: true
layout: post
title: FasterCGI with HHVM
category: blog
redirect_from:
  - /blog/1817/fastercgi-with-hhvm
---

Today, we are happy to announce [FastCGI](http://www.fastcgi.com/drupal/) support for HHVM. FastCGI is a popular protocol for communication between an application server (e.g. running your PHP code) and a webserver. With support for FastCGI, you will be able to run HHVM behind any [popular web server](http://en.wikipedia.org/wiki/FastCGI#Web_Servers_that_implement_FastCGI) (Apache, Nginx, Lighttpd, etc). The webserver is in charge of handling all the intricate details of the HTTP protocol. HHVM is in charge of what it does best, running PHP code blazingly fast.


<!--truncate-->

If you can’t wait to get your hands on the new feature, just jump to the Installation section. If you are curious about how the new feature was baked into HHVM or just want to learn how well it performs, read on.


# How it works




FastCGI was designed to solve one crucial problem that plagued its predecessor CGI, namely: performance. The CGI protocol required that a new instance of the application be spawned on every request. Such a trade-off could have been tolerable for small native programs where start-up overhead was negligible. It is however incredibly difficult for a JIT compiler such as HHVM. The HipHop virtual machine keeps track of the code that ran in the past and reuses bytecode output whenever it sees a known file. HHVM also performs just-in-time compilation, i.e. translates snippets of the bytecode into native machine code when they are run frequently. Both of these features require that an instance of HHVM runs in server mode and lives on from request to request. FastCGI protocol enables that. Moreover, FastCGI can be configured to reuse the same connection for serving multiple requests. This involves serving both requests coming one after another and serving multiple requests in parallel. In the latter case data from multiple requests is multiplexed on a single connection.




HHVM FastCGI server uses asynchronous I/O. This means that an I/O thread will never block waiting on a single connection. Instead, system routines such as select() are used to monitor activity on multiple connections at once. When activity is detected (e.g. file descriptor becomes ready for reading or writing), an I/O thread executes the appropriate non-blocking action. This completes a single cycle of the event loop. This approach maximizes CPU use when serving I/O. Consequently, the threads spend only as much time blocked as absolutely necessary. I/O is served using multiple threads. Once the server is under heavy load, there will roughly be one I/O thread per CPU core. The incoming connections are then distributed evenly between the I/O threads using a round robin. As a result, operations on a single connection are always single-threaded and no additional synchronisation is needed.




A separate set of worker threads is used to execute PHP code. All the (partially) decoded requests are put inside a common concurrent queue. In a loop, each worker thread then pops a new request to be served. At this point, all the request headers are ready. For small requests, the request body will also typically be available. When a request is large (e.g. is a file upload), the worker thread might block waiting on more I/O to become available. The payload can be stored to a file in order to keep memory usage low. Once all the request data becomes available, PHP execution may begin. The output produced by a PHP script is buffered and sent to an I/O thread for further handling.





# Performance




We conducted benchmarks using Nginx. In the first test we ran a Wordpress instance. The second test showcases HHVM performance for computation-intensive tasks. We used a simple php script computing Fibonacci numbers.





## Wordpress




The first test was performed using the Wordpress example page. No changes were made to the wordpress deployment besides filling in mandatory database connection fields. Nginx was used as a web server. Apache bench was used for load testing using this command:





    ab -c 50 -n 1000 http://localhost/wordpress/wordpress/?p=1




### PHP-FPM


Sadly the results were pretty bad for PHP. Only 23 requests per second seem to indicate that Wordpress is computationally very expensive to run in an interpreter.


    Requests per second: 23.17 [#/sec] (mean)
    Time per request:    2157.579 [ms] (mean)
    Time per request:    43.152 [ms] (mean, across all concurrent requests)
    Transfer rate:       275.42 [Kbytes/sec] received




### HHVM FastCGI




On a cold start, HHVM still performed much better than PHP-FPM; however, there was a clear penalty associated with the initial JITing of PHP files:





    Requests per second: 184.71 [#/sec] (mean)
    Time per request:    270.689 [ms] (mean)
    Time per request:    5.414 [ms] (mean, across all concurrent requests)
    Transfer rate:       2194.38 [Kbytes/sec] received




After the initial warm-up the results got noticeably better:





    Requests per second: 949.21 [#/sec] (mean)
    Time per request:    52.676 [ms] (mean)
    Time per request:    1.054 [ms] (mean, across all concurrent requests)
    Transfer rate:       11276.46 [Kbytes/sec] received




That’s a surprisingly good result of roughly 40x higher throughput than the default PHP-FPM setting.





## Fibonacci




Next we decided to compare the two runtimes using a computationally expensive example. We wrote a simple function computing Fibonacci numbers using an exponential algorithm. Here are the results for computing Fib(N) for value N = 5, 15, 25, 30:





### PHP-FPM




    Requests per second: 13789.24 [#/sec] (mean) Fib(5)
    Requests per second: 3202.31 [#/sec] (mean)  Fib(15)
    Requests per second: 118.94 [#/sec] (mean)   Fib(25)*
    Requests per second: 8.40 [#/sec] (mean)     Fib(30)**




*only 1000 requests were performed to save time




**only 100 requests were performed to save time





### HHVM FastCGI




    Requests per second: 8842.70 [#/sec] (mean) Fib(5)
    Requests per second: 8892.66 [#/sec] (mean) Fib(15)
    Requests per second: 5581.37 [#/sec] (mean) Fib(25)
    Requests per second: 737.56 [#/sec] (mean)  Fib(30)




In case where N = 5, the page required almost no computation at all. In this case it was visible just how well optimized FPM really is. It was over 50% faster than HHVM FastCGI server which indicates that there is still a lot of room for improvement in our implementation. However at N = 15 the amount of computation already shifted the balance to HHVM’s advantage. Where for HHVM the bottleneck was still the network, FPM was clearly CPU bound at this point with a result almost 3x worse than HHVM. At N = 30, HHVM just in time compilation really shined, yielding results almost 80x faster than PHP.





# Installation




Now to the fun part: how to get HHVM FastCGI working on your machine? For popular Debian-based distros we prepared a set of pre-built packages:





### Ubuntu 12.04




    echo deb http://dl.hhvm.com/ubuntu precise main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm




### Ubuntu 13.10




    echo deb http://dl.hhvm.com/ubuntu saucy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm




### Debian 7




    echo deb http://dl.hhvm.com/debian wheezy main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm




### Other




If your distro is not on the list, you can still run HHVM FastCGI, with slightly more work (or you can take the scripts from that package and repackage it for your distro). First, install the [latest release of HHVM](https://github.com/facebook/hhvm/wiki#installing-pre-built-packages-for-hhvm). To run the server in FastCGI mode, pass additional parameters to HHVM runtime:





    cd /path/to/your/www/root
    hhvm --mode server -vServer.Type=fastcgi -vServer.Port=9000




The server will now accept connections on localhost:9000 (only TCP sockets are supported for now). To turn the server into a daemon, change the value of mode to:





    hhvm --mode daemon -vServer.Type=fastcgi -vServer.Port=9000




All the usual options accepted by the HHVM runtime are also available in the FastCGI mode. Please make sure that HHVM runs from the directory where you wish to serve PHP files.




Once the HHVM FastCGI server is up and running, it’s time to appropriately configure your webserver of choice. As an example, we include instructions for Apache and Nginx.





## Making it work with Apache




The recommended way of integrating with Apache is using the mod_proxy_fcgi module. First, you need to enable mod_proxy and mod_proxy_fcgi modules, if you haven’t done so already. To enable the modules make sure you have the following symlinks created:





    cd /path/to/your/apache/conf
    ln -s ../mods-available/mod_proxy.load mods-enabled/mod_proxy.load
    ln -s ../mods-available/mod_proxy.conf mods-enabled/mod_proxy.conf
    ln -s ../mods-available/mod_proxy_fcgi.load mods-enabled/mod_proxy_fcgi.load




Next up, you need to insert a directive instructing Apache to send traffic to the FastCGI server. You can do so by inserting the following line in your apache.conf / httpd.conf file.





    ProxyPass / fcgi://127.0.0.1:9000/path/to/your/www/root/goes/here/




Please note that this will route _all_ the traffic to the FastCGI server. If you want to route only certain requests (e.g. only those from a subdirectory or ending *.php, you can use ProxyPassMatch, e.g.





    ProxyPassMatch ^/(.*.php(/.*)?)$ fcgi://127.0.0.1:9000/path/to/your/www/root/goes/here/$1




Consult [Apache docs](http://httpd.apache.org/docs/trunk/mod/mod_proxy_fcgi.html) for more details on how to use ProxyPass and ProxyPassMatch.





## Making it work with Nginx




The default FastCGI configuration from Nginx should work just fine with HHVM FastCGI. You will need to add the following directives inside one of your location directives:





    root /path/to/your/www/root/goes/here;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME /path/to/your/www/root/goes/here$fastcgi_script_name;
    include        fastcgi_params;




The traffic for the surrounding location directive will then be routed to HHVM.





# What’s next?




There are a couple of important features still missing from the initial implementation. The most notable is support for local UNIX sockets. At present, only less performant (however more flexible) TCP sockets are available. The priorities for this release were:







  * Correctness,


  * Getting the architecture of the solution right, so that performance can be improved in the future.


We haven’t really done any profiling on the new server yet. It is therefore quite likely that there is some low hanging fruit waiting to be picked. We are definitely looking forward to improving HHVM FastCGI performance in the future releases.
