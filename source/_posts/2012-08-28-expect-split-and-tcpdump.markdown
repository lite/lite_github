---
layout: post
title: "expect-split-and-tcpdump"
date: 2012-08-28 20:25
comments: true
categories: 
---

# tcpdump
  
    tcpdump -x -vv  -i en0 "tcp port 8001"

SuSE:    

    tcpdump port 8001 -X -vv
    
# expect

ssh_config:
    
    host test
        user app100642705
        hostname 10.1.2.15 
        port 3322
        identityfile pkey

myshell.sh:

    #!/usr/bin/expect -f
    spawn ssh -F ssh_config test
    expect "*(yes/no)?" {
        send "yes\r"
    }
    interact #expect eof

# split

    tar -czvf - test | split -b 50m - test.tar.gz
    cat test.tar.gz.a* > - | tar -zxvf - 