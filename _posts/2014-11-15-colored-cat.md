---
layout: post
title: Colored `cat`
published: True
categories: [linux]
tags: [terminal,cat,pygments]
---

The post is based on Paul Irish's video -> [Paul Irish on Web Application Development Workflow](https://www.youtube.com/watch?v=vDbbz-BdyYc)
Ever wanted a nice colored output of the `cat` command in the terminal? Here it is how you can fulfill your 'dream' :)

# Pygmentize cat

Install pygments

    $ sudo apt-get install python-pygments

Set an alias in `.bashrc`

    alias c="pygmentize -g"

Use it

    $ c users.json

Screenshot

![pygmentized_cat](/assets/pygments.png)