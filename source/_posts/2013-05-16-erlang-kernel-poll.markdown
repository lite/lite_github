---
layout: post
title: "nodejs, C libevent and erlang"
date: 2013-05-16 00:41
comments: true
categories: [nodejs, erlang]
---

nodejs < libevent < erlang

	node.js:  connect=10000,active connect=100,req=1378370,time=60,req/sec=22972.8,msec/req=4.35543
	libevent: connect=10000,active connect=100,req=3719106,time=60,req/sec=61985.1,msec/req=1.61258
	erlang:	  connect=10000,active connect=100,req=6377574,time=60,req/sec=106293,msec/req=0.939882

## node_test.js

<pre><code>
	var net = require('net');
	var cnt = 0;
	var server = net.createServer(function (socket) {
	  socket.pipe(socket);
	});

	server.listen(8000, "127.0.0.1");
</code></pre>

## libevent_test.c

<pre><code>
	#include < stdlib.h>
	#include < unistd.h>
	#include < netinet/in.h>  
	#include < sys/socket.h>  
	#include < sys/types.h>  
	#include < sys/socket.h>
	#include < event.h>  
	#include < stdio.h>  
	#include < time.h> 
	#include < string.h>
	#include < fcntl.h>

	int buf_len = 2048;
	int msg_len = 1024; 
	int total = 0;

	int setnonblock(int fd)
	{       
		int flags;       
		flags = fcntl(fd, F_GETFL);       
		if (flags < 0)               
			return flags;       
		flags |= O_NONBLOCK;       
		if (fcntl(fd, F_SETFL, flags) < 0)               
			return -1;       
	 
		return 0;
	}

	void connection_echo(int fd, short event, void *arg)
	{
		struct event *ev = (struct event *)arg;
		event_add(ev, NULL);

		char buf[buf_len];
		int read_len = read(fd, buf, msg_len);
		write(fd, buf, read_len);
	}

	void connection_accept(int fd, short event, void *arg)   
	{ 
	    /* for debugging */ 
	    fprintf(stderr, "%s(): fd = %d, event = %d,	total = %d.\n", __func__, fd, event, ++total);  

	    /* Accept a new connection. */ 
	    struct sockaddr_in s_in;  
	    socklen_t len = sizeof(s_in);  
	    int ns = accept(fd, (struct sockaddr *) &s_in, &len);  
	    if (ns < 0) {  
	        perror("accept");  
	        return;  
	    }  

		setnonblock(ns);

	    /* Install echo server. */ 
	    struct event *ev = (struct event *)malloc(sizeof(struct event));  
	    event_set(ev, ns, EV_READ, connection_echo, ev);  
	    event_add(ev, NULL);  
	} 

	int main(void)  
	{  
	    /* Request socket. */ 
	    int s = socket(PF_INET, SOCK_STREAM, 0);  
	    if (s < 0) {  
	        perror("socket");  
	        exit(1);  
	    }  

	    /* bind() */ 
	    struct sockaddr_in s_in;  
	    memset(&s_in, 0, sizeof(s_in));  
	    s_in.sin_family = AF_INET;  
	    s_in.sin_port = htons(8000);  
	    s_in.sin_addr.s_addr = INADDR_ANY;  
	    if (bind(s, (struct sockaddr *) &s_in, sizeof(s_in)) < 0) {  
	        perror("bind");  
	        exit(1);  
	    }  

	    /* listen() */ 
	    if (listen(s, 1000) < 0) {  
	        perror("listen");  
	        exit(1);  
	    }  

	    /* Initial libevent. */ 
	    event_init();  

	    /* Create event. */ 
	    struct event ev;  
	    event_set(&ev, s, EV_READ | EV_PERSIST, connection_accept, &ev);  

	    /* Add event. */ 
	    event_add(&ev, NULL);  

	    event_dispatch();  

	    return 0;  
	}
</code></pre>

## erlang_test.erl

In Eshell:

	1>c(erlang_test).
	2>erlang_test:start().

<pre><code>
	-module(erlang_test).
	-export([start/0]).

	start() ->
	        {ok, Listen} = gen_tcp:listen(8000, [binary,
	                                                %{packet, 4},
	                                                {reuseaddr, true},
	                                                {backlog, 2000},
	                                                {active, true}]),
	        spawn(fun() -> par_connect(Listen, 0) end).

	par_connect(Listen, Count) ->
	        {ok, Socket} = gen_tcp:accept(Listen),
	        New = Count + 1,
	        io:format("Accept succ ~p~n", [New]),
	        spawn(fun() -> par_connect(Listen, New) end),
	        loop(Socket).


	loop(Socket) ->
	    receive
	        {tcp, Socket, Bin} ->
	            gen_tcp:send(Socket, Bin),
	            loop(Socket);
	        {tcp_closed, Socket} ->
	            io:format("Server socket closed~n")
	    end.
</code></pre>
