---
layout: post
title: "wget JDK with cookie "
date: 2013-09-29 10:54
comments: true
categories: JDK
---

"In order to download products from Oracle Technology Network you must agree to the OTN license terms" 
You need a single cookie to bypass this:
 
  Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F

JDK7

  wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F" http://download.oracle.com/otn-pub/java/jdk/7u25-b15/jdk-7u25-macosx-x64.dmg

JDK6

  wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F" http://download.oracle.com/otn-pub/java/jdk/6u45-b06/jdk-6u45-linux-i586-rpm.bin