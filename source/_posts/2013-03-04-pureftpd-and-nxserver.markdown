---
layout: post
title: "pureftpd and nxserver"
date: 2013-03-04 18:57
comments: true
categories: 
---

## pureftpd

	./configure --prefix=/usr/local/pureftpd --with-puredb 
	make && make install
	mkdir /usr/local/pureftpd/etc
	groupadd ftpgroup
	useradd -g ftpgroup -d /dev/null -s /etc ftpuser
	cp configuration-file/pure-ftpd.conf /usr/loca/pureftpd/etc/
	cp configuration-file/pure-config.pl /usr/loca/pureftpd/sbin/
	chmod +x /usr/loca/pureftpd/sbin/pure-config.pl
	/usr/local/pureftpd/bin/pure-pw useradd test -u ftpuser -d /data/ftp/
	/usr/local/pureftpd/bin/pure-pw mkdb

Modify PureDB in "/usr/loca/pureftpd/etc/pure-ftpd.conf"

	PureDB                    /usr/local/pureftpd/etc/pureftpd.pdb
	PassivePortRange          30000 50000

Enable port in "/etc/sysconfig/SuSEfirewall2"

    FW_SERVICES_EXT_TCP="21 30000:50000"

Reload firewall config

    SuSEfirewall2

Startalone pureftpd

	/usr/loca/pureftpd/sbin/pure-config.pl /usr/loca/pureftpd/etc/pure-ftpd.conf

## nxserver

Download [nxserver](http://www.nomachine.com/download.php)

Add user

	/usr/NX/bin/nxserver --useradd nxuser

nxclient login as a normal user "nxuser"
