---
layout: post
title: "nodejs on aliyun"
date: 2013-04-25 13:54
comments: true
categories: [nodejs, aliyun]
---

Mount the data disk

	fdisk /dev/xvdb
	mkfs.ext3 /dev/xvdb1
	echo '/dev/xvdb1  /mnt ext3    defaults    0  0' >> /etc/fstab
	mount -a

Install the requirements by yum

	sed -i "s/exclude=kernel*/#exclude=kernel*/g" /etc/yum.conf
	yum update
	yum install git gcc-c++ openssl-devel make

Install nodejs

	wget -N http://nodejs.org/dist/node-latest.tar.gz
	tar xzvf node-latest.tar.gz && cd `ls -rd node-v*`
	./configure
	make install

Install coffeescript and forever by npm

	npm install coffeescript
	npm install forever
	forever start -w app.js
