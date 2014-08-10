---
layout: post
title: Google-Chrome on Ubuntu-12.04 (Precise Pangolin)
published: true
categories: [linux]
tags: [ubuntu, googlechrome]
---

Usually Chrome can't be found in the ubuntu repositories, so we need to install it by hand.

## Installation

Download .deb package from [google](https://href.li/?http://www.google.com/intl/hu/chrome/browser/)

    $ sudo dpkg -i google-chrome-stable_current_amd64.deb
    $ sudo apt-get -f install

If after the `dpkg` the system calls for a missing `libcurl3` package, try

    $ sudo apt-get -f install
