---
layout: post
title: Capturing screenshots of websites from terminal
published: true
categories: [linux]
tags: [linux,terminal,screenshot]
---

[pageres](https://github.com/sindresorhus/pageres) is a handy tool for capturing screenshots of your websites, or capturing a screenshot of any website. The cool thing is, that you can capture your site running under localhost, like

```bash
jim-y@linuxws:~/projects/hybrid/phonegap/cordova.rainyday$ pageres http://localhost:8080/android/www/#/ 1366x768

✔ Generated 1 screenshot from 1 url and 1 resolution
```

`pageres` generated a file named *localhost!8080!android!www!#-1366x768.png* under the current directory. Neat! :)