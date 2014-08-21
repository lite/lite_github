---
layout: post
title: "expect，split和tcpdump"
date: 2012-08-28 20:25
comments: true
categories: [技巧]
---

# [tcpdump](http://danielmiessler.com/study/tcpdump/)

<pre>  
tcpdump -x -vv  -i any "tcp port 8001"
tcpdump -X -vv -s 4096  -w portrange.cap 'portrange 8001-8005'
tcpdump -X -vv -s 4096  -w ip.cap -i any 'src 8.8.8.8 or dst 6.6.6.6'
tcpdump -r host.cap -XX -s 4096 > host.cap.txt  
</pre>

# expect

ssh_config内容
    
<pre>
host test
    user app100642705
    hostname 10.1.2.15 
    port 3322
    identityfile pkey
</pre>

myshell.sh内容

<pre>
#!/usr/bin/expect -f
spawn ssh -F ssh_config test
expect "*(yes/no)?" {
    send "yes\r"
}
interact #expect eof
</pre>

# split

<pre>
tar -czvf - test | split -b 50m - test.tar.gz
cat test.tar.gz.a* > - | tar -zxvf - 
</pre>
