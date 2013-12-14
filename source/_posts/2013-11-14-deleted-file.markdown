---
layout: post
title: "deleted file"
date: 2013-11-14 11:14
comments: true
categories: 
---

You deleted the file, but disk space is not free.
30439 is the pid and 1w is the fd.

<pre>
lsof | grep deleted
java      30439 root    1w      REG              202,1 3522641920     360788 /root/nohup.out (deleted)
</pre>

Clear the file.

<pre>
echo "" > /proc/30439/fd/1
</pre>
