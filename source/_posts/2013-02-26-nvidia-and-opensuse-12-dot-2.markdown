---
layout: post
title: "nvidia and openSUSE 12.2"
date: 2013-02-26 22:59
comments: true
categories: 
---

Install these packages by zypper

	zypper in kernel-devel 
	zypper in kernel-desktop-devel
	zypper in kernel-source
	zypper in gcc

Update /etc/modprobe.d/50-blacklist.conf

	#blacklist nvidiafb
	blacklist nouveau

Install nvidia driver
	
	sudo sh ./NVIDIA.run