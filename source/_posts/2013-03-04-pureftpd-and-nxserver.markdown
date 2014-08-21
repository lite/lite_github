---
layout: post
title: "pureftpd 和 nxserver"
date: 2013-03-04 18:57
comments: true
categories: [运维]
---

## 配置pureftpd

<pre>
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
</pre>

修改"/usr/loca/pureftpd/etc/pure-ftpd.conf"的 PureDB 

<pre>
PureDB                    /usr/local/pureftpd/etc/pureftpd.pdb
PassivePortRange          30000 50000
</pre>

在"/etc/sysconfig/SuSEfirewall2"中启用端口

<pre>
FW_SERVICES_EXT_TCP="21 30000:50000"
</pre>

重新加载防火墙配置

<pre>
SuSEfirewall2
</pre>

启动pureftpd

<pre>
/usr/loca/pureftpd/sbin/pure-config.pl /usr/loca/pureftpd/etc/pure-ftpd.conf
</pre>

## 配置nxserver

下载 [nxserver](http://www.nomachine.com/download.php)

添加用户

<pre>
/usr/NX/bin/nxserver --useradd nxuser
</pre>

nxclient 用户登录： "nxuser"
