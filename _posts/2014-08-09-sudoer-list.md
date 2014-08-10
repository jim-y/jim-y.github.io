---
layout: post
title: Sudoer list
published: true
categories: [linux]
tags: [cli, terminal, debian]
---

Open up a root terminal, and type 

    $ visudo

search for the section *# User privilege specification* and extend it with our new user

    jim ALL=(ALL:ALL) ALL

After the process, the user `jim` should have sudo rights. Read [more](https://wiki.debian.org/sudo) about this, on the Debian Wiki.