---
layout: post
title: "pmset_hibernatemode"
date: 2014-05-21 19:08
comments: true
categories: [技巧]
---

关闭深度睡眠，当mac没电时候，系统会自动进入深度休眠，把内存放到硬盘上相同大小的空间中，很少用到也占用硬盘空间。

查看深度休眠模式，3表示有深度休眠
<pre>
sudo pmset -g | grep hibernatemode
</pre>

关闭深度休眠
<pre>
sudo pmset -a hibernatemode 0
</pre>

删除深度休眠创建的内存映像文件：
<pre>
sudo rm /var/vm/sleepimage
</pre>
