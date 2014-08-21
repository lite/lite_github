---
layout: post
title: "nginx支持gzip"
date: 2012-10-15 22:44
comments: true
categories: [运维]
---

修改 conf/nginx.conf，添加 gzip 支持

<pre>
gzip            on;
gzip_comp_level 5;
gzip_min_length 1024;
gzip_types      text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript image/jpeg image/gif image/png;
gzip_proxied    expired no-cache no-store private auth;
gzip_disable    "MSIE [1-6]\.";
</pre>

重新加载 nginx

<pre>
sbin/nginx -s reload
</pre>

测试

<pre>
curl -I --compressed http://fssle.com/8/config/txt/task.xml
</pre>
