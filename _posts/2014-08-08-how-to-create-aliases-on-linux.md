---
layout: post
title: How to create aliases on Linux
published: true
categories: [linux]
tags: [cli, terminal]
---

Did you ever feel, that typing `cd ..` all the time to go back to the previous directory is just a pain in the ass? Then aliases are created for you.

## The Problem

I always faced with the problem, that I typed faster than typing correctly, so i usually mistyped `cd ..` to `cd..` or `cd.` and this misspells just blowed up my mind. I wanted something that would be easier to type.

## The Solution

aliases were made to overcome this kind of problems. We can create alias commands (commands with a different name, but with the same outcome. Technically typing the new alias name just calls the original command).

### .bashrc

You can define your own aliases in a hidden file called .bashrc (the *dot* before the filename shows that this file is hidden) located in your home directory. Let's open it up, and make some aliases:

These are my own aliases. I found `cls` better/faster than `clear` and also `..` is much more easier for me than `cd ..`

{% highlight bash %}
alias ll='ls -lF'
alias la='ls -laF'
alias l='ls -CF'
alias cls="clear;date"
alias cd..="cd .."
alias ..="cd .."
alias del="trash-put"
alias nanoc="nano -Y nanorc"
{% endhighlight %}