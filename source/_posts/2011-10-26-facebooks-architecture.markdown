---
layout: post
title: "facebook's architecture"
date: 2011-10-26 00:56
comments: true
categories: [Architecture]
---

[facebook's architecture on quora](http://www.quora.com/What-is-Facebooks-architecture)

+ Web front-end written in PHP. Facebook's HipHop [1] then converts it to C++ and compiles it using g++, thus providing a high performance templating and Web logic execution layer
+ Business logic is exposed as services using Thrift [2]. Some of these services are implemented in PHP, C++ or Java depending on service requirements (some other languages are probably used...)
+ Services implemented in Java don't use any usual enterprise application server but rather use Facebook's custom application server. At first this can look as wheel reinvented but as these services are exposed and consumed only (or mostly) using Thrift, the overhead of Tomcat, or even Jetty, was probably too high with no significant added value for their need.
+ Persistence is done using MySQL, Memcached [3], Facebook's Cassandra [4], Hadoop's HBase [5]. Memcached is used as a cache for MySQL as well as a general purpose cache. Facebook engineers admit that their use of Cassandra is currently decreasing as they now prefer HBase for its simpler consistency model and its MapReduce ability.
+ Offline processing is done using Hadoop and Hive
+ Data such as logging, clicks and feeds transit using Scribe [6] and are aggregating and stored in HDFS using Scribe-HDFS [7], thus allowing extended analysis using MapReduce
+ BigPipe [8] is their custom technology to accelerate page rendering using a pipelining logic
+ Varnish Cache [9] is used for HTTP proxying. They've prefered it for its high performance and efficiency [10].
+ The storage of the billions of photos posted by the users is handled by Haystack, an ad-hoc storage solution developed by Facebook which brings low level optimizations and append-only writes [11].
+ Facebook Messages is using its own architecture which is notably based on infrastructure sharding and dynamic cluster management. Business logic and persistence is encapsulated in so-called 'Cell'. Each Cell handles a part of users ; new Cells can be added as popularity grows [12]. Persistence is achieved using HBase [13].
+ Facebook Messages' search engine is built with an inverted index stored in HBase [14]
+ Facebook Search Engine's implementation details are unknown as far as I know
+ The typeahead search uses a custom storage and retrieval logic [15]
+ Chat is based on an Epoll server developed in Erlang and accessed using Thrift [16]
+ About the resources provisioned for each of these components, some information and numbers are known:
+ Facebook is estimated to own more than 60,000 servers [17]. Their recent datacenter in Prineville, Oregon is based on entirely self-designed hardware [18] that was recently unveiled as Open Compute Project [19].
+ 300 TB of data is stored in Memcached processes [20]
+ Their Hadoop and Hive cluster is made of 3000 servers with 8 cores, 32 GB RAM, 12 TB disks that is a total of 24k cores, 96 TB RAM and 36 PB disks [20]
+ 100 billion hits per day, 50 billion photos, 3 trillion objects cached, 130 TB of logs per day as of july 2010 [21]

