---
layout: post
title: "rebar usage"
date: 2014-03-06 18:01
comments: true
categories: [erlang]
---

Create server

    rebar create-app appid=lyapp
    rebar compile
    rebar clean
    rebar create template=simplesrv srvid=lyapp_server

Eunit

    mkdir -p test

    lyapp_test.hrl：
    -include_lib("eunit/include/eunit.hrl").
    my_test() ->
    	?assert(1 + 1 =:= 2).

    rebar compile eunit

Rel

    mkdir -p rel
    rebar create-node nodeid=lyapp

    rebar.config:
    {sub_dirs, ["rel"]}.

Build

    rebar compile
    rebar generate
    rel/lyapp/bin/lyapp start
    rel/lyapp/bin/lyapp stop 
    rel/lyapp/bin/lyapp console
    > application:which_applications().
    > release_handler:which_releases().
