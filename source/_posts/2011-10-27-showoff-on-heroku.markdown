---
layout: post
title: "heroku上使用showoff"
date: 2011-10-27 20:46
comments: true
categories: [运维]
---

[showoff](https://github.com/schacon/showoff)

<pre>
heroku config:add SHOWOFF_EVAL_RUBY=1

showoff create . -d ruby
showoff add title -d ruby
showoff serve
showoff heroku slide
</pre>

[showoff-io](http://showoff.io/)

<pre>
show 9090
</pre>
