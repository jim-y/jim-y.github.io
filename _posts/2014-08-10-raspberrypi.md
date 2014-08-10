---
layout: post
title: Raspberrypi
published: true
categories: [linux]
tags: [rpi, raspberrypi, smarthome]
---

The `Raspberry Pi` is a credit-card sized computer that plugs into your TV and a keyboard. It is a capable little computer which can be used in electronics projects, and for many of the things that your desktop PC does, like spreadsheets, word-processing and games It also plays high-definition video. We want to see it being used by kids all over the world to learn how computers work, how to manipulate the electronic world around them, and how to program.

## Getting the image

I recommend Raspbian which is Debian's port to RPI. Under Ubuntu, one can burn the image to the SD-Card via `ImageWriter`. As an alternative, you can always choose `dd`. We love dd :)

    $ sudo dd bs=4M if=/home/user/Downloads/raspbian.img of=/dev/sdx

## Initial Settings

[Settings](https://href.li/?http://mattwilcox.net/archives/setting-up-a-secure-home-web-server-with-raspberry-pi/)

## Saving RPI hostname

Usually if you have a PI at home, you will frequently log-in through ssh. Normally it would look like: `ssh 192.168.1.102`, after a few weeks this will start to getting a pain in the ass. So one could save an 'alias' pointing to RPI. Open `/etc/hosts` and write

    192.168.1.102 raspberrypi

After this, we will be able to reach RPI as `raspberrypi`.

## Remote login

Remote login via [ssh-rsa](https://www.linode.com/docs/security/securing-your-server/)

