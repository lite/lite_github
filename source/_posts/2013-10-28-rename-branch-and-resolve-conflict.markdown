---
layout: post
title: "rename branch and resolve conflict"
date: 2013-10-28 00:03
comments: true
categories: [git]
---

* Rename remote branch

<pre>
git branch -m old_branch new_branch
git push origin :old_branch
git push origin new_branch
</pre>

* Resolve conflict

<pre>
git checkout --ours .
git checkout --theirs .
</pre>