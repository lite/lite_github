---
layout: post
title: "配置阿里云服务器"
date: 2013-04-25 13:54
comments: true
categories: [运维]
---

加载数据盘

<pre>
fdisk /dev/xvdb
mkfs.ext3 /dev/xvdb1
echo '/dev/xvdb1  /mnt ext3    defaults    0  0' >> /etc/fstab
mount -a
</pre>

使用yum安装所需包

<pre>
sed -i "s/exclude=kernel*/#exclude=kernel*/g" /etc/yum.conf
yum update
yum install git gcc-c++ openssl-devel make
</pre>

安装nodejs

<pre>
wget -N http://nodejs.org/dist/node-latest.tar.gz
tar xzvf node-latest.tar.gz && cd `ls -rd node-v*`
./configure
make install
</pre>

使用npm安装coffeescript和forever

<pre>
npm install coffeescript
npm install forever
forever start -w app.js
</pre>