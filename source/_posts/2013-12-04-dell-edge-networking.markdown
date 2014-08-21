---
layout: post
title: "DELL edge 网络配置"
date: 2013-12-04 12:05
comments: true
categories: [运维]
---

修改 /etc/sysconfig/network-scripts/ifcfg-em1

<pre>
ONBOOT=yes  #no
</pre>

重启服务

<pre>
service network restart
</pre>
    