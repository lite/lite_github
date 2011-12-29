---
layout: post
title: "octopress on heroku"
date: 2011-10-25 00:56
comments: true
categories: [Octopress, Heroku]
---

[blogging](http://octopress.org/docs/blogging/)

    rake generate
    rake preview

[heroku](http://octopress.org/docs/deploying/heroku/)

    heroku create lite
    git remote add heroku git@heroku.com:lite.git
    rake new_post[octopress]
    git push heroku master
