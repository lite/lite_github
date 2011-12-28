---
layout: post
title: "zte_ct_x920 on ubuntu"
date: 2011-12-28 16:51
comments: true
categories: [ubuntu, android]
---
[android udev](http://blog.163.com/dengjingniurou@126/blog/static/5398919620111112111659617/)

adb devices

```
List of devices attached
????????????    no permissions
```

lsusb

```
Bus 001 Device 050: ID 19d2:ffda ONDA Communication S.p.A. 
```

sudo vim /etc/udev/rules.d/51-Android.rules

```
SUBSYSTEM=="usb", SYSFS{idVendor}=="19d2", MODE="0666"
```

sudo chmod a+r /etc/udev/rules.d/51-Android.rules
sudo /etc/init.d/udev stop
sudo /etc/init.d/udev start

then re-plug the cable

adb devices

```
List of devices attached 
X920_CT device
```
