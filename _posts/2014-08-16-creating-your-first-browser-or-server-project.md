---
layout: post
title: "Creating your first browser/server module - PART 1"
published: true
categories: [javascript]
tags: [npm,node,bower,jshint,grunt,browserify,requirejs]
---

In this blog post i will guide you trough of the first few steps of creating a new JavaScript module, either aiming for the browser -as a client library-, or targeting the server -as a nodejs module-. In this example, we will create a new project from the ground (this process is called *scaffolding*, you should check [yeoman](http://yeoman.io/) after this tutorial) we will create the requisite project structure, and we will be creating the basics of such a module. We will call our project **Sam** (from *Sam*ple, noob, i know :D)

## Prerequisites

You will need [nodejs](http://nodejs.org/) installed on your system ([Install nodejs on Debian]({% post_url 2014-08-10-install-nodejs-on-debian %})). We will use nodejs npm-modules as dependencies in **Sam**. `node` is JavaScript for the server. You can write JavaScript modules which can interact with the file system, you can exec shell commands, and basically you can make any I/O related job in nodejs very well. In fact, nodejs is very useful when you are facing with a(n) I/O task, because of its non-blocking event-driven nature.

You will need [npm](https://www.npmjs.org/) also. Read the [manual](https://www.npmjs.org/doc/README.html) to insall it. npm is node's package manager, you can install 3rd party node modules with it. Some say, that npm is simply the best package manager out there.

[Bower](http://bower.io/) will also be handy, but its not mandatory for us now. Why bower? We have `npm` for installing node modules, modules that will be handy when we are doing server related stuff, but what about our client (browser) related dependencies? This is, where `bower` kicks-in. Install it by typing

    $ npm install -g bower

Last, but not least, you should install a good IDE/Editor if you doesn't have one yet. I would recommend JetBrains's **WebStorm** which is simply the *uber-alles* IDE for frontend web-development, but sadly its not free. So, you should stick with Sublime, Atom, or Brackets in my opinion. I will use `sublime`.

### Sublime Text

Sublime Text is a highly configurable text-editor ideal for JavaScript development. You can choose from many syntax highlighting, themes, packages, etc. In another post, i will cover some of its basic settings.

## Sam

Okay, so we set up our environment by installing `node`, `npm`, and `bower`, and we have a good text-editor. We can now start implementing the project. First of all, Sam, our sample project will be a jQuery-like client side library with some npm based features. In other words, we will create a new, but very simple JavaScript library with dependencies both from browser side, and from server side. Our client side dependency will be `jQuery`, and for the simplicity, our server side npm dependency will be `mpromise`.

## GitHub

We will create a repository for Sam on GitHub, so you will need a repository, and/or an account there. For this sample, i created a repository, which is accessible @[https://github.com/jim-y/sam](https://github.com/jim-y/sam)

## Start with npm

As a kickstart, create a new directory on your file system for Sam. I recommend to create a `projects` directory under your home folder for such projects.

```bash
$ mkdir projects/Sam
```

Go to the folder, and type

    $ npm init

npm's startup wizard will be shown, and you will be guided to create your new npm package. **Wait, what?** We are creating a client side package not a server-side package, you should tell, but the truth is, that creating a private (not published) npm package will serve us some handy stuff, like automation, linting, minification, etc. In short, we can say, that we are creating a server side package just to be able to produce our client-side library as an end-product easier.

```bash
jim@linwst430:~/projects/Sam$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sane defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (Sam) 
version: (0.0.0) 0.0.1
description: jQuery like client-side library with mpromises
entry point: (index.js) lib/sam.js
test command: grunt test
git repository: https://github.com/jim-y/sam.git
keywords: promises jquery sam browser dom-traversing
license: (ISC) MIT
About to write to /home/jim/projects/Sam/package.json:

{
  "name": "Sam",
  "version": "0.0.1",
  "description": "jQuery like client-side library with mpromises",
  "main": "lib/sam.js",
  "scripts": {
    "test": "grunt test"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/jim-y/sam.git"
  },
  "keywords": [
    "promises",
    "jquery",
    "sam",
    "browser",
    "dom-traversing"
  ],
  "author": "Attila Kling <attila.kling@gmail.com>",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/jim-y/sam/issues"
  },
  "homepage": "https://github.com/jim-y/sam"
}


Is this ok? (yes)
```

Now install our npm dependencies. We will use `mpromise` as a 'real' depenedency, so install it with

    $ npm install mpromise --save

The `--save` flag will tell npm to append a new entry for this dependency in the package.json file. But we will need some development dependencies like a build tool, a minification tool, a linting tool, etc. We will install them very similar.

```bash
$ npm install grunt grunt-contrib-jshint grunt-contrib-watch grunt-contrib-uglify grunt-contrib-jasmine grunt-browserify --save-dev
```

Now, we have a directory structure like this:

```bash
.
├── node_modules
│   ├── grunt
│   ├── grunt-browserify
│   ├── grunt-contrib-jasmine
│   ├── grunt-contrib-jshint
│   ├── grunt-contrib-uglify
│   ├── grunt-contrib-watch
│   └── mpromise
└── package.json
```

Also check the `package.json` file to identify the new fields. The node_modules folder is the place, where our npm packages will be held. Both the dev-, and real dependencies.

#### Short overview 

* `grunt` is a JavaScript build tool for frontend web-development. We will use it for task automation.
* `browserify` is a module system, with its help, we can import our dev modules as CommonJS packages. Read more later
* `jasmine` is a test system what we will use in this project
* `jshint` - our tool for linting JavaScript code
* `uglify` - our minification tool
* `watch` - our live reload helper tool, more on this later

## Initialize git

Next, initialize our git repository in our project folder, by

    $ git init

We also need to set up our remote repository to be able to pull, push.

    $ git remote add origin https://github.com/jim-y/sam.git

Make sure that the command made the changes, by

    $ git remote -v

The result should be

```bash
origin  https://github.com/jim-y/sam.git (fetch)
origin  https://github.com/jim-y/sam.git (push)
```

Remember, that previously you created a new GitHub repository, as i made it with Sam, and you will probably have there a `README.md`, and a `.gitignore` file. We don't have them yet in the local copy, so try to initially sync your working directory with your github repo by pulling the repo:

    $ git pull origin master

As a result, that should pull down these two files from the remote repository.

## Initialize bower

This process is very similar that npm's init was.

    $ bower init

Then add the same properties, as we added before.

```bash
jim@linwst430:~/projects/Sam$ bower init
[?] name: Sam
[?] version: 0.0.1
[?] description: jQuery like client-side library with mpromises
[?] main file: lib/sam.js
[?] what types of modules does this package expose? 
[?] keywords: 
[?] authors: Attila Kling <jimmyfly10@gmail.com>
[?] license: MIT
[?] homepage: https://github.com/jim-y/sam
[?] set currently installed components as dependencies? Yes
[?] add commonly ignored files to ignore list? Yes
[?] would you like to mark this package as private which prevents it from being accidentally published to the registry? Yes

{
  name: 'Sam',
  version: '0.0.1',
  authors: [
    'Attila Kling <jimmyfly10@gmail.com>'
  ],
  description: 'jQuery like client-side library with mpromises',
  main: 'lib/sam.js',
  license: 'MIT',
  homepage: 'https://github.com/jim-y/sam',
  private: true,
  ignore: [
    '**/.*',
    'node_modules',
    'bower_components',
    'test',
    'tests'
  ]
}

[?] Looks good? (Y/n) y
```

Our `bower.json` file was successfully created, we are able now to install jQuery as a dependency.

    $ bower install jquery --save

This command will create a `bower_components` folder, and jquery in it. At this time, our package looks as follows:

```bash
.
├── bower_components
│   └── jquery
├── bower.json
├── .git
├── .gitignore
├── node_modules
│   ├── grunt
│   ├── grunt-browserify
│   ├── grunt-contrib-jasmine
│   ├── grunt-contrib-jshint
│   ├── grunt-contrib-uglify
│   ├── grunt-contrib-watch
│   └── mpromise
├── package.json
└── README.md
```

If something is missing for you, please read the related paagraph again. But here is a short overview of these files/folders.

* bower_components created by addressing `bower init` && `bower install jquery --save`
* .git created by typing `git init`
* .gitignore was pulled down from the remote repository
* node_modules was created upon `npm install *`
* package.json by `npm init`
* README.md was pulled down from the github repo

## Continue on creating the project structure

As a next step, create a `lib` folder for our main JavaScript file `sam.js`. Make a `test` folder for our tests, and place a `spec` folder inside it. Also extend the project with a `.jshintrc` file by

    $ wget https://gist.githubusercontent.com/haschek/2595796/raw/500806cafd239ace8dc94c998a8d4f7270947b12/.jshintrc

and a `.editorconfig` by creating the file: `sublime .editorconfig` and paste the following code in it:

```ini
# EditorConfig is awesome: http://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
end_of_line = lf
insert_final_newline = true

# 4 space indentation
[*.py]
indent_style = space
indent_size = 4

# Tab indentation (no size specified)
[*.js]
indent_style = tab

# Indentation override for all JS under lib directory
[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

The gist was copied from [example](http://editorconfig.org/#example-file). The jshintrc file defines your linting rules, that is, when you will run your jshint tasks via grunt (more about this later), grunt will search for this file and it will lint your code according to these rules. The editorconfig file helps setting your indentation rules among different IDE-s.

## Overview

That was PART-1, we created the basic structure of our project, we initialized npm, bower and git to be able to start coding. In the next chapter we will start implementing sam.js, i will introduce you grunt, and what we can do with it.

Stay tuned.