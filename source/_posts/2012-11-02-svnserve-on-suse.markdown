---
layout: post
title: "svnserve on SuSE"
date: 2012-11-02 21:10
comments: true
categories: [SuSE, svn]
---

Create the repos
    
    groupadd svn; useradd -d /srv/svn -s /bin/false -g svn svn
    
Enable 3690 port /etc/sysconfig/SuSEfirewall2
    
    FW_SERVICES_EXT_TCP="22 80 3306 3690"
    
Create the repos

    svnadmin create /srv/svn/repos

Configuration  

    ;/srv/svn/repos/conf/svnserve.conf   
    [general]
    anon-access = none
    auth-access = write
    password-db = passwd

    ;/srv/svn/repos/conf/passwd
    [users]
    test = test
    
    ;/etc/sysconfig/svnserve
    ;The -R option enforces read-only access
    SVNSERVE_OPTIONS="-d -r /srv/svn/repos"
    
Start svnserve

    chown -R svn:svn /srv/svn/
    chmod -R 755 /srv/svn/
    chkconfig svnserve
    service svnserve start
    
On svn client working

    svn co --username test svn://192.168.1.21/ my-repos
    svn up
    svn merge ./ -r 5:4 
    svn st
    svn commit -m "rollback to r4"