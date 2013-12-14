---
layout: post
title: "dell edge networking"
date: 2013-12-14 12:05
comments: true
categories: [ops]
---

Modify /etc/sysconfig/network-scripts/ifcfg-em1

<pre>
ONBOOT=yes  #no
</pre>

Then restart network service

<pre>
service network restart
</pre>
    