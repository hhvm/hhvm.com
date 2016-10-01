---
author: sgolemon
comments: true
layout: post
title: The AdminServer
category: blog
redirect_from:
  - /blog/521/the-adminserver
---

HipHop, if properly configured [1], will actually startup not one, but two http servers.  The first, on port 80 by default, you're already familiar with.  Requests are translated to filesystem paths, and PHP files are executed to generate content.  The other one, however, you might not have come across yet.

<!--truncate-->

This second http server allows you, as the administrator, to take action through a web browser similar to the apachectl command.  This interface can enable/disable/display various statistics, dump jit translations and apc values, and even instruct the server to shut itself down.

> [1] HipHop builds prior to Dec 10, 2012 had the AdminServer enabled by default.  If you do not wish to have this running, you should add AdminServer.Port = 0 to your config file.


## Enabling the AdminServer


Turning it on is actually just a one-line change to your config file, but since it provides administrator type functionality, it's best to set a password as well, and probably a firewall to block unwanted traffic.


    AdminServer {
      Port = 8080
      Password = superSecret
    }


For firewalls, I find linux's iptables do the trick nicely.  These two lines allow access from localhost, but drop any other packets bound for the admin server from elsewhere.


    iptables -A INPUT -i lo -j ACCEPT
    iptables -A INPUT -p tcp --destination-port 8080 -j DENY




## Getting a list of commands


Just browse to the AdminServer's port and you'll get a text/plain dump of the available commands and their usage.  For the purpose of these examples, I'll be using cURL from the command line.


    $ curl 'http://localhost:8080'


Some commands, like_ /stats-web_ are binary switches, calling once will turn them 'On' (indicating you've enabled it), calling again will return 'Off'.  Others, like_ /check-health_ will give you info on HipHop's internal workings in JSON (or HTML or XML) format.


    $ curl 'http://localhost:8080/check-health'




    {
      "load":1.52
    ,  "queued":0
    ,  "tc-size":544
    ,  "tc-stubsize":358
    ,  "targetcache":20480
    ,  "units":1
    }




## Password authorization


If you set a password in your configuration, then all queries to the AdminServer (apart from /help or no command at all) will require that password be passed with the request, e.g.:


    curl 'http://localhost:8080/check-health?auth=superSecret'


Generally speaking, however, you should probably firewall your AdminServer or disable it entirely (by setting Port=0).
