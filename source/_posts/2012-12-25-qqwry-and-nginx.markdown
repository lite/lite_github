---
layout: post
title: "QQwry and Nginx"
date: 2012-12-25 14:50
comments: true
categories: [DevOps]
---

clone the modules from github

    git clone git://github.com/anjuke/ngx_http_qqwry_module.git
    git clone git://github.com/agentzh/echo-nginx-module.git

compile nginx

    ./configure --with-debug --add-module=./ngx_http_qqwry_module/ --add-module=./echo-nginx-module/
    make

download [qqwry](http://update.cz88.net/soft/qqwry.rar)
convert qqwry.dat.gbk to qqwry.dat(utf8), and copy to nginx/conf folder.

    python qqwry_iconv.py

edit nginx.conf

    http {
        qqwry $remote_addr $qqwry_loc /conf/qqwry.dat;

        server {
            charset utf-8;

            location /hello {
                echo $remote_addr;
                echo $qqwry_loc; 
                if ($qqwry_loc ~ "浙江省北京市四川省成都市"){
                    echo "hello";
                }
            }
        }
    }

start nginx

    objs/nginx -c conf/nginx.conf

