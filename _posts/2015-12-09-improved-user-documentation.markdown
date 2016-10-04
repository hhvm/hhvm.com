---
author: joelm
comments: true
layout: post
title: Improved User Documentation
category: blog
permalink: /blog/10925/improved-user-documentation
---

We are happy to announce our next generation of Hack and HHVM user documentation available at [http://docs.hhvm.com](http://docs.hhvm.com).

<!--truncate-->

Back in August, we announced that we are going full force in revamping user documentation. We sent out a public survey to gauge the standing on the existing documentation at the time. We had 160 responses to the survey. Those results served as both validation and a guide to our approach with the new documentation.

The key takeaways from the survey results were as follows:




  * The existing documentation is generally good, but could use improvement.


  * The look and feel of the site could use work.


  * [Async](http://docs.hhvm.com/hack/async/introduction), [Collections](http://docs.hhvm.com/hack/collections/introduction) and the [Type System](http://docs.hhvm.com/hack/types/introduction) could use better content.


  * More sample code, a clear [API reference](http://docs.hhvm.com/hack/reference/) and feature tutorials are must haves.


  * The examples were not runnable or sometimes even wrong.


  * No more docbook.


We believe we have made big improvements to all these areas.


## New GitHub Repo


We have a [new GitHub repo](https://github.com/hhvm/user-documentation) for the documentation. The name "user-documentation" reflects that this documentation is focused primarily to the users of Hack and HHVM. This repo contains [content](https://github.com/hhvm/user-documentation/tree/master/guides), the [source code](https://github.com/hhvm/user-documentation/tree/master/src) to render the site, and detailed README information for [running the site locally](https://github.com/hhvm/user-documentation/blob/master/README.md) and [contributing content](https://github.com/hhvm/user-documentation/blob/master/CONTRIBUTING.md).


## Site Structure


These docs have been written from the ground up, both from content and infrastructure. There are three main sections consisting of two user guides and one API reference:




  * Hack - [http://docs.hhvm.com/hack/](http://beta.docs.hhvm.com/hack/)


  * Hack API reference - [http://docs.hhvm.com/hack/reference/](http://l.facebook.com/l.php?d=AQGCRSXKixSeI4Bb-wOTsVg5eQg7bZ_mDbBb5yBbXn8t2JFaoV5SvyNi-64&u=http%3A%2F%2Fbeta.docs.hhvm.com%2Fhack%2Freference%2F&h=eAQHBXDGwAQHV_1Njlvt6j0vYZ3EJYciK7Cy2LsPbE2OC-w&enc=AZOuKBNLpY6nRXb5dTR5RH4j_WFXj91tehdU5hSzt_mlGgmI8XfO5IXjzfaMXCXOIqmlquh8iky1qgjfWzZquDxMwLegWnhzWMbeB-Hy9-xq6iftlIo0oMTyk1zm4HQeVqTQUyN7UMpuQkd9iDL1OsPvijKIeBz-Fn9CBdfIB_y11Q&s=1)


  * HHVM - [http://docs.hhvm.com/hhvm/](http://beta.docs.hhvm.com/hhvm/)


The guides provide "what" and "how-to" information on a variety of topics, including code examples.

The API reference is a raw class and method reference for everything we have added to Hack. There is documentation for each class, each method on a class and for stand-alone functions, many of which will also include an example.

It is worth noting that the old documentation combined a copy of the [http://php.net](http://php.net) documentation with the specific documentation for Hack and HHVM. This caused two problems. First, the PHP-specific documentation could become stale if updates were made on the php.net side. Secondly, this could confuse readers who may think that this was Hack and HHVM specific documentation since search engines linked to our website for that documentation in many cases. To solve this, we are intentionally not including the [php.net](http://php.net) information in our documentation; instead we will be redirecting requests to those pages to the actual [php.net](http://php.net) source of truth.


## Site Technology


The source code that generates the site is written _entirely_ in Hack, referencing some third-party libraries that are written in Hack, PHP and other languages. This is a real-world use of Hack -- the generation of the Hack and HHVM documentation with the Hack programming language.


#### Documentation


The API documentation is generated from the various [HHI](https://github.com/facebook/hhvm/tree/master/hphp/hack/hhi), [HNI](https://github.com/facebook/hhvm/tree/master/hphp/runtime/ext) and [Systemlib](https://github.com/facebook/hhvm/tree/master/hphp/system/php) files that exist in the HHVM source code -- i.e., code is the source of truth for the API reference.

All of the guides are written in _markdown_, which we will feel is a much more user friendly format than the docblock representation in the previous documentation. And this will also be more amenable to users of the documentation to provide [issues](https://github.com/hhvm/user-documentation/issues) and [pull requests](https://github.com/hhvm/user-documentation/pulls).


#### Examples


Unless it is an explicit code snippet to support documentation, all of our examples are [_runnable_ code](https://github.com/hhvm/user-documentation#running-the-examples). You can copy and paste the code and run it directly with [HHVM](http://docs.hhvm.com/hhvm/) and the [Hack typechecker](http://docs.hhvm.com/hack/typechecker/introduction). We have also made all of our examples compatible with the [HHVM test runner](https://github.com/hhvm/user-documentation#using-the-hhvm-test-runner). This helps ensure that all our examples produce the expected output, from both an HHVM and Hack perspective.


#### Site Generation


In a nutshell, the site generation code does two main things. On the raw API side, it uses reflection on the HHVM codebase to produce a Hack/HHVM/PHP-agnostic intermediate YAML format format, which in turn generates the Markdown documentation for the class and function signatures, etc. Then, all of the markdown, including that from the the guide and API commentary side, is converted to HTML.

Another benefit of the YAML production is that we hope to re-use this framework for other languages/projects in the future.

After dependency installation, the entire [build process](https://github.com/hhvm/user-documentation#local-site-installation) takes on the order of less than one minute, so forking and testing changes to the documentation should be nearly painless.


## Feedback


Please have a look around the new site. For a short period of time, you may see a survey banner at the top of the documentation pages. We would really appreciate your feedback on the new site through this survey so that we ensure that we met the quality bar we tried to achieve with this revamp.

If you see any problems on a particular documentation page, please use the issue link at the bottom of that page to file a GitHub issue. For any general problems, please [file an issue](https://github.com/hhvm/user-documentation/issues) directly.

**Thank you and enjoy!**
