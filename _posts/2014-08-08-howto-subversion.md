---
layout: post
title: How-to Subversion
published: true
categories: [linux]
tags: [cli, terminal, subversion, svn, version-control]
---

Subversion is a version control system, widely used by Enterprises. It makes the collaboration easier among project members. Read [more]({{ page.url }})

{% comment %}
Long posts (> 300 wordcount) should give a "Read more" link in the excerpt
{% endcomment %}

## Installation[![permalink](/assets/permalink.png)]({{page.url}}#installation)

From repository

```bash
$ sudo apt-get update
$ sudo apt-get install subversion
```

Optionally create the repository on a flash drive

```bash
$ sudo mkdir /media/pendrive/svn/repo
$ sudo mkdir /tmp/repo
$ sudo mkdir /tmp/repo/branches
$ sudo mkdir /tmp/repo/tags
$ sudo mkdir /tmp/repo/trunk
$ sudo svnadmin create /media/pendrive/svn/repo
$ sudo svn import /tmp/repo file:///media/pendrive/svn/repo -m "initial import"
$ sudo rm -rf /tmp/repo
```

## Settings[![permalink](/assets/permalink.png)]({{page.url}}#settings)

1. edit password file & add users
2. edit `authz` file (optional)
3. set up `svnserve.conf`

### 1

```bash
$ sudo nano passwd

# add users
[users]
myname = mypasswd
```

### 2

```bash
$ sudo nano authz

# Edit authz file
[/]
* =
myname = rw
```

The * mark means every other users, and we make the repo root directory (/) unreachable for them. For the user `myname` we make the repository readable/writeable.

### 3

```bash
$ sudo nano svnserve.conf

# Set these
[general]
anon-access=none
auth-access=write
password-db=passwd
authz-db=authz
realm=My Repository
```

## Startup[![permalink](/assets/permalink.png)]({{page.url}}#startup)

```bash
$ svnserve -d -r /media/pendrive/svn/
```

Ckeck, if the daemon started successfully

```bash
$ ps auxww | fgrep svnserve
```

Read more about [svnserve](https://href.li/?http://svnbook.red-bean.com/en/1.6/svn.serverconfig.svnserve.html)

## Configuring the router[![permalink](/assets/permalink.png)]({{page.url}}#configuring-the-router)

SVN is listening on port 3690 on default for every incoming requests over `svn://` protocol. But first we need to portforward every incoming request to the raspberrypi. Mind, that before we already binded 192.168.1.102 to the PI, so on the port forwarding give this inner ip.

## More on SVN[![permalink](/assets/permalink.png)]({{page.url}}#more-on-svn)

```bash
$ svn co svn://domain/repo localcopyfolder
$ svn update (up)
$ svn add
$ svn import
$ svn remove (rm)
$ svn commit
$ svn revert
$ svn status (st)
$ svn log
$ svn info
``` 

## A more easier guide

First install subversion on the server side, and client side aswell.
    
    $ sudo apt-get install subversion

Next, on server side, create a directory to hold our repository(ies).

    $ sudo mkdir /web/svn/

Next, create our repo.

    $ svnadmin create /web/svn/repo

Next, set up basic authentication, edit svnserve.conf file and uncomment password-db = passwd line.

    $ sudo nano -Y nanorc /web/svn/repo/conf/svnserve.conf

Next, add some user to the passwd file.

    $ sudo nano -Y nanorc /web/svn/repo/conf/passwd

Next, start the svnserve daemon.

    $ svnserve -d -r /web/svn/

To check if it started properly,
    
    $ netstat -tap | grep svn , or
    $ ps auxww | fgrep svnserve

Next add the svn port to the routers port forwarding table. bind port 3690 to the server machine’s IP.
Next, checkout the repo on the client machine,

    $ svn co --username svn:///repo LocalFolder

## Tips & Tricks

Counting commits by user

    $ svn log | egrep uname | wc -l