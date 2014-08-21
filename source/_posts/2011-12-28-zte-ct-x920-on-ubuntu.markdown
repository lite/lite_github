---
layout: post
title: "Ubuntu上使用zte_ct_x920"
date: 2011-12-28 16:51
comments: true
categories: [技巧]
---
[android udev](http://blog.163.com/dengjingniurou@126/blog/static/5398919620111112111659617/)

运行 adb devices 

<pre>
List of devices attached
????????????    no permissions
</pre>

运行 lsusb

<pre>
Bus 001 Device 050: ID 19d2:ffda ONDA Communication S.p.A. 
</pre>

编辑 /etc/udev/rules.d/51-Android.rules

<pre>
SUBSYSTEM=="usb", SYSFS{idVendor}=="19d2", MODE="0666"
</pre>

重启udev

<pre>
sudo chmod a+r /etc/udev/rules.d/51-Android.rules
sudo /etc/init.d/udev stop
sudo /etc/init.d/udev start
</pre>

重新插入X920_CT

运行adb devices

<pre>
List of devices attached 
X920_CT device
</pre>
