---
layout: post
title: "vagrant 和 veewee"
date: 2011-10-31 23:51
comments: true
categories: [运维] 
---

[vagrant](http://vagrantup.comi)

[veewee](https://github.com/jedi4ever/veewee)
    
<pre>
vagrant basebox templates
mkdir iso
vagrant basebox define 'fssle' 'ubuntu-11.04-server-i386'
vagrant basebox build 'fssle'
vagrant basebox validate 'fssle'
vagrant basebox export 'fssle'
vagrant box add 'fssle' 'fssle'
vagrant init 'fssle'
vagrant up
vagrant reload
vagrant ssh
</pre>
