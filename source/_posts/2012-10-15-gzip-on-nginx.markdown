---
layout: post
title: "gzip on nginx"
date: 2012-10-15 22:44
comments: true
categories: [DevOps]
---

add gzip support in conf/nginx.conf

    gzip            on;
    gzip_comp_level 5;
    gzip_min_length 1024;
    gzip_types      text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript image/jpeg image/gif image/png;
    gzip_proxied    expired no-cache no-store private auth;
    gzip_disable    "MSIE [1-6]\.";

reload nginx

    sbin/nginx -s reload

test by curl

    curl -I --compressed http://fssle.com/8/config/txt/task.xml