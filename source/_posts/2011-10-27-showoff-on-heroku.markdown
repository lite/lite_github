---
layout: post
title: "showoff on heroku"
date: 2011-10-27 20:46
comments: true
categories: [heroku, showoff, showoff-io]

---

[showoff](https://github.com/schacon/showoff)

    heroku config:add SHOWOFF_EVAL_RUBY=1

    showoff create . -d ruby
    showoff add title -d ruby
    showoff serve
    showoff heroku slide

[showoff-io](http://showoff.io/)

    show 9090

