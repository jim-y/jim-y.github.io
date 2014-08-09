---
layout: post
title: JavaScript interpreters
published: true
categories: [javascript]
tags: [nodejs, spidermonkey, js, chrome-dev-tools]
---

JavaScript is an interpreted language. While developing JavaScript sorces we face with the problem, that interpreting the code, or in other words, to check our modifications needs sometimes too much steps. e.g reloading the webpage, importing sources to our html, making our page ready for debugging some newly created code, etc.

In this post, i will show you some tools, interpreters to overcome these problems.

## Running JavaScript[![permalink](/assets/permalink.png)]({{page.url}}#running-javascript)

### Command line interface

On Debian system `spidermonkey` standalone JavaScript interpreter is still available

    $ sudo apt-get install spidermonkey-bin
    $ js -i
    $ js -f mycode.js

> SpiderMonkey is Mozilla's JavaScript engine written in C/C++. It is used in various Mozilla products, including Firefox, and is available under the MPL2. Read [more](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey)

On Ubuntu you can however install `nodejs`

    $ sudo apt-get install nodejs
    $ node
    $ node mycode.js

> Node.js® is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices. Read [more](http://nodejs.org/)

### Browser

Your browser has a built-in JavaScript interpreter, so you dont need to explicitly "build" your code. You just wrap your code in the HTML site, and the browser does its job. The JavaScript engine built-in Chrome is named `V8`, and the one built-in Mozilla is named `SpiderMonkey`. As an alternative way in the browser you can open up the browser's developer-tools console (`F12` on Chrome, `Ctrl+Shift+K` on Firefox) and you can type any valid JavaScript statement in the console.

### 3rd party tools

On 3rd party tools i mean like Scratchpad for Firefox. Scratchpad is a standalone JavaScript code editor and interpreter built on the top of Firefox. You can open it up pressing `Shift+F4` in Firefox.