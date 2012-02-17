---
layout: post
title: "archlinux on vmware"
date: 2012-02-17 04:35
comments: true
categories: [Archlinux, Vmware]
---

## Enable networking

append to /etc/rc.conf
  
    eth0="dhcp"
    INTERFACE=(eth0)
    ROUTES=(!gateway)

run command "/etc/rc.d/network restart"

## Enable pacman repo

append to "/etc/pacman.conf"

    SigLevel=Optional TrustAll 

uncomment the repo in "/etc/pacman.d/mirrorlist" 

## Upgrade  
    
    pacman -Syu
