---
layout: post
title: Install node on Debian
published: true
categories: [linux]
tags: [debian, nodejs, javascript]
---

When a package is not present in the repository, or its on a very outdated version, it could be hard to get the right package. In this post we will inspect two alternatives to get nodejs on your debian powered system.

For Debian Wheezy, you have two options:

### Build from source

```bash
$ sudo apt-get install python g++ make checkinstall
$ src=$(mktemp -d) && cd $src
$ wget -N http://nodejs.org/dist/node-latest.tar.gz
$ tar xzvf node-latest.tar.gz && cd node-v*
$ ./configure
$ sudo checkinstall -y --install=no --pkgversion $(echo $(pwd) | sed -n -re's/.+node-v(.+)$/\1/p') make -j$(($(nproc)+1)) install
$ sudo dpkg -i node_*
```

### Uninstall

    $ sudo dpkg -r node

### Backports

Alternatively, you can install nodejs from wheezy-backports. If you rely on having node as an executable, install nodejs-legacy as well. If you need npm as well, you can get it through the installer

    $ curl https://www.npmjs.org/install.sh | sudo sh