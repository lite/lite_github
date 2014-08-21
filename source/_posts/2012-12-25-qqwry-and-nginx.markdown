---
layout: post
title: "Nginx下使用QQwry"
date: 2012-12-25 14:50
comments: true
categories: [运维]
---

下载nginx模块

<pre>
git clone git://github.com/anjuke/ngx_http_qqwry_module.git
git clone git://github.com/agentzh/echo-nginx-module.git
</pre>

编译 nginx

<pre>
./configure --with-debug --add-module=./ngx_http_qqwry_module/ --add-module=./echo-nginx-module/
make
</pre>

下载 [qqwry](http://update.cz88.net/soft/qqwry.rar)

转换 qqwry.dat.gbk to qqwry.dat(utf8), 复制到文件夹 nginx/conf.

<pre>
python qqwry_iconv.py
</pre>

编辑 nginx.conf

<pre>
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
</pre>

启动 nginx

<pre>
objs/nginx -c conf/nginx.conf
</pre>
