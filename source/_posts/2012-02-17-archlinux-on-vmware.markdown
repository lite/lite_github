---
layout: post
title: "Vmware上使用archlinux"
date: 2012-02-17 04:35
comments: true
categories: [技巧]
---

## 启动网络

修改 /etc/rc.conf

<pre>  
eth0="dhcp"
INTERFACE=(eth0)
ROUTES=(!gateway)
</pre>

重启网络 "/etc/rc.d/network restart"

## 启用 pacman 仓库

修改 "/etc/pacman.conf"

<pre>
SigLevel=Optional TrustAll 
</pre>

注释 "/etc/pacman.d/mirrorlist" 

## 更新包

<pre>    
pacman -Syu
</pre>