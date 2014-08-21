---
layout: post
title: "heroku上使用octopress "
date: 2011-10-25 00:56
comments: true
categories: [运维]
---

[blogging](http://octopress.org/docs/blogging/)

<pre>
rake generate
rake preview
</pre>

[heroku](http://octopress.org/docs/deploying/heroku/)

<pre>
heroku create lite
git remote add heroku git@heroku.com:lite.git
rake new_post[octopress]
git push heroku master
</pre>
