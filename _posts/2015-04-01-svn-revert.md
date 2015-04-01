---
layout: 
title: svn revert
categories: [linux]
tags: [svn,subversion,revert]
published: True

---

Reverting a revision from subversion turned out to be pretty easy. So the use case is when you made some breaking changes say in `rev. 1160` and you need to revert only that particular revision.

```bash
svn merge -c -1160 .
```

The "-" sign before the revision number is mandatory! After this command you need to commit the revert again.