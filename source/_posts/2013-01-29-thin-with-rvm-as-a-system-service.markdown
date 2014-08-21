---
layout: post
title: "Rvm下使用thin"
date: 2013-01-29 22:04
comments: true
categories: [运维]
---

安装thin 到 /etc/init.d/thin

<pre>
rvm wrapper ruby-1.9.2-p125 bootup thin
sudo  ~/.rvm/bin/bootup_thin install
</pre>

编辑 /etc/init.d/thin 的 DAEMON 

<pre>
DAEMON=/usr/local/bin/bootup_thin
</pre>

在 runlevel 3 和 5 启动 thin

<pre>
sudo /sbin/chkconfig -s thin 35
</pre>

编辑 /etc/thin/thin.yml

<pre>
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
</pre>
	
启动 thin 服务

<pre>	
sudo /sbin/service thin start
</pre>
