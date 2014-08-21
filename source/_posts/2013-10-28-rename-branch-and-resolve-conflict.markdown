---
layout: post
title: "Git使用技巧"
date: 2013-10-28 00:03
comments: true
categories: [技巧]
---

* 重命名远程分支

<pre>
git branch -m old_branch new_branch
git push origin :old_branch
git push origin new_branch
</pre>

* 解决冲突

<pre>
git checkout --ours .
git checkout --theirs .
</pre>