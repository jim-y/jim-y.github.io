---
layout: post
title: Scan opened ports with netcat
published: true
categories: [linux]
tags: [cli, netcat]
---

    $ nc -z -w1 localhost 10-8000

If we want to get additional information about opened ports

    $ echo “” | nc -v -w1 localhost 10-50