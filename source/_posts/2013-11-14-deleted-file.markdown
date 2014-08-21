---
layout: post
title: "删除文件未释放空间"
date: 2013-11-14 11:14
comments: true
categories: [技巧]
---

删除了文件，但磁盘没有释放。
pid是30439，fd是1w。

<pre>
lsof | grep deleted
java      30439 root    1w      REG              202,1 3522641920     360788 /root/nohup.out (deleted)
</pre>

清除该文件

<pre>
echo "" > /proc/30439/fd/1
</pre>
