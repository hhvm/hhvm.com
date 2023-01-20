---
title: "CVE-2022-36937: TLS 1.0 connections"
layout: post
author: wilfred
category: blog
---


We've just released patch releases for HHVM: 4.172.1, 4.168.2 and
4.153.4. These resolve the security issue CVE-2022-36937.

The functions `stream_sock_server` and `stream_socket_client` (part of
the stream extension) accept URLs. When a URL starts with `tls://`
these would previously allow TLS 1.0 connections.

TLS 1.0 is deprecated and considered insecure. As of these new
releases, `stream_sock_server` and `stream_socket_client` only permit
newer TLS connections.
