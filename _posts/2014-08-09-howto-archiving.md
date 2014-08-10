---
layout: post
title: How-to Archiving
published: true
categories: [linux]
tags: [cli, terminal, zip, tar, compress]
---

## Archive into tar[![permalink](/assets/permalink.png)]({{page.url}}#archive-into-tar)

Recursive compression on directory

    $ tar -zcvf dest.tar.gz source/

* -z archive to gz
* -c create
* -v verbose
* -f archive filename

Decompress files to current directory

    $ tar -zxvf source.tar.gz

## Archive into zip[![permalink](/assets/permalink.png)]({{page.url}}#archive-into-zip)

Recursive compression of a directory

    $ zip -r dest source

As an example, dest would be woowie.zip, and source could be woowie/ (dir)