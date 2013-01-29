---
layout: post
title: "thin with rvm as a system service"
date: 2013-01-29 22:04
comments: true
categories: [thin, rvm]
---

Install thin to /etc/init.d/thin

	rvm wrapper ruby-1.9.2-p125 bootup thin
	sudo  ~/.rvm/bin/bootup_thin install

Edit DAEMON in /etc/init.d/thin
	DAEMON=/usr/local/bin/bootup_thin

Enable thin system service at runlevel 3 and 5 

	sudo /sbin/chkconfig -s thin 35

Edit /etc/thin/thin.yml

	pid: tmp/pids/thin.pid
	wait: 30
	port: 8000
	timeout: 30
	log: log/thin.log
	max_conns: 1024
	require: []
	environment: production
	max_persistent_conns: 512
	daemonize: true
	servers: 3
	socket: /tmp/thin.sock
	chdir: /home/dli/dth/redmine
	
Start service thin
	
	sudo /sbin/service thin start
