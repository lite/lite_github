---
layout: post
title: "SUSE上安装nvidia驱动"
date: 2013-02-26 22:59
comments: true
categories: [技巧]
---

使用zypper安装包

<pre>
zypper in kernel-devel 
zypper in kernel-desktop-devel
zypper in kernel-source
zypper in gcc
</pre>

更新 /etc/modprobe.d/50-blacklist.conf

<pre>
#blacklist nvidiafb
blacklist nouveau
</pre>

安装 nvidia 驱动

<pre>	
sudo sh ./NVIDIA.run
</pre>