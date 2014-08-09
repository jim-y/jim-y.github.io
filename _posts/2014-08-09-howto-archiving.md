---
layout: post
title: How-to Archiving
published: true
categories: [linux]
tags: [cli, terminal, zip, tar, compress]
---

## Archive into tar

Recursive **compression** on directory

    tar -zcvf dest.tar.gz source/

* -z archive to gz
* -c create
* -v verbose
* -f archive filename

**Decompress** to current directory

    tar -zxvf source.tar.gz

## Archive into zip

> Tags: {{ page.tags | sort | array_to_sentence_string }}