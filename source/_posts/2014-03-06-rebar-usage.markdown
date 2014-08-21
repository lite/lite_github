---
layout: post
title: "rebar工具"
date: 2014-03-06 18:01
comments: true
categories: [脚本]
---

# 创建服务器

<pre>
rebar create-app appid=lyapp
rebar compile
rebar clean
rebar create template=simplesrv srvid=lyapp_server
</pre>

# 测试

<pre>
rebar compile eunit
</pre>

lyapp_test.hrl内容

</pre>
-include_lib("eunit/include/eunit.hrl").
my_test() ->
    ?assert(1 + 1 =:= 2).
</pre>

# 发行
    
<pre>
rebar create-node nodeid=lyapp
</pre>

rebar.config内容

<pre>
{sub_dirs, ["rel"]}.
</pre>

# 编译运行

<pre>
rebar compile
rebar generate
rel/lyapp/bin/lyapp start
rel/lyapp/bin/lyapp stop 
rel/lyapp/bin/lyapp console
> application:which_applications().
> release_handler:which_releases().
</pre>
