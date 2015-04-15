---
layout: post
title: svn revert
categories: [linux]
tags: [svn,subversion,revert]
published: true

---

Reverting a revision from subversion turned out to be pretty easy. So the use case is when you made some breaking changes say in `rev. 1160` and you need to revert only that particular revision.

```bash
svn merge -c -1160 .
```

The "-" sign before the revision number is mandatory! After this command you need to commit the revert again.

And what about the case when you need to recommit your revertion? :D To make it clear:

- commited a revision, like 1160
- you needed to revert it -> `svn merge -c -1160 .`
- now you need to reverse merge it -> `svn merge -c 1160 . --ignore-ancestry`

Pretty nice, but not so straightforward :/