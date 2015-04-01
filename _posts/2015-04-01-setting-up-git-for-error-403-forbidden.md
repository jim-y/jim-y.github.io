---
layout: post
title: Setting up git for Error 403 Forbidden
categories: [linux]
tags: [git,error,forbidden]
published: true
---

```bash
$ git push origin master
error: The requested URL returned error: 403 Forbidden while accessing https://github.com/jim-y/jim-y.github.io.git/info/refs

fatal: HTTP request failed
```

If the upper error is familiar then most probably you are on the right place to find the solution. I could come over this by editing the `.git/config` file and replace 

```bash
[remote "origin"]
	fetch = +refs/heads/*:refs/remotes/origin/*
	url = https://github.com/jim-y/jim-y.github.io.git
```

with

```bash
[remote "origin"]
	fetch = +refs/heads/*:refs/remotes/origin/*
	url = https://jim-y@github.com/jim-y/jim-y.github.io.git
```

Mind the only modification in the url by appending my user name after `https://`.