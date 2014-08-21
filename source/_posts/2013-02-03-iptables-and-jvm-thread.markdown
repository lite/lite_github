---
layout: post
title: "Iptables 和 JVM thread"
date: 2013-02-03 13:12
comments: true
categories: [运维]
---

[Iptables](http://www.dd-wrt.com/wiki/index.php/Iptables_command)

	iptables -L
	iptables -F

	iptables -I INPUT -p TCP -m multiport --dports 8001:8005 -j REJECT 
    iptables -I INPUT -p TCP -m multiport --dports 8001:8005 -s 8.8.0.0/16 -j ACCEPT
    
    iptables -I OUTPUT -p TCP -d 10.142.20.0/24 -j REJECT

[JVM thread limit]

	-Xms   intial java heap size
	-Xmx   maximum java heap size
	-Xss   the stack size for each thread
	
	/proc/sys/kernel/pid_max
	/proc/sys/kernel/thread-max
	max_user_process（ulimit -u）
	/proc/sys/vm/max_map_count
