---
layout: post
title: "Amazon EC2上安装Git服务器"
date: 2012-12-06 16:57
comments: true
categories: [运维]
---

[Run your own Git server with Gitolite and Amazon EC2](http://edvanbeinum.com/run-your-own-git-server-with-gitolite-and-amazon-ec2)

创建用户

<pre>
useradd git -g wheel --create-home --shell /usr/bin/git-shell
</pre>

修改 sshd_config

<pre>
AllowUsers git
</pre>

安装 gitolite

<pre>
sudo yum -y install perl-CPAN perl-Time-HiRes

perl -MCPAN -e shell
    o conf urllist http://cpan.yahoo.com/
    o conf commit
    install CPAN
    reload cpan

git clone git://github.com/sitaramc/gitolite
mkdir -p $HOME/bin
gitolite/install -to $HOME/bin
bin/gitolite setup -pk YourName.pub
</pre>
            
使用ssh测试git

<pre>
ssh -i dli.pem ec2-user@aws
ssh -Nqf -D 7070 -i dli.pem ec2-user@aws
git clone aws:gitolite-admin.git
git clone aws:testing.git
</pre>
