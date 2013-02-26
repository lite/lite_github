---
layout: post
title: "expect-split-and-tcpdump"
date: 2012-08-28 20:25
comments: true
categories: [shell]
---

# [tcpdump](http://danielmiessler.com/study/tcpdump/)
  
    tcpdump -x -vv  -i any "tcp port 8001"
    tcpdump -X -vv -s 4096  -w portrange.cap 'portrange 8001-8005'
    tcpdump -X -vv -s 4096  -w ip.cap -i any 'src 8.8.8.8 or dst 6.6.6.6'
    tcpdump -r host.cap -XX -s 4096 > host.cap.txt  

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