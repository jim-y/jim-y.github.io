---
layout: post
title: Terminal F.A.Q
published: true
categories: [linux]
tags: [cli, terminal, bash, commands]
---

The linux terminal is a powerful tool what every linux user should learn to use.

## Tweaks

### Colors

Edit `.bashrc` and search for `#force_color_prompt=yes`, uncomment it. Then set color by editing

```sh
if [ "$color_prompt" = yes ]; then
  PS1=’${debian_chroot:+($debian_chroot)}\[33[01;32m\]\u@\h\[33[00m\]:\[\
```

Read [more](https://href.li/?http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)

### Commands

Create own command by defining a new function.

```bash
$ function cdls(){ cd $1; ls -l; }
```

Usage `cdls directory/`

### Horizontal rule

The [project](https://href.li/?https://github.com/LuRsT/hr). If already not exists, create a ~/bin/ directory, and perform these commands:

```bash
$ curl https://raw.github.com/LuRsT/hr/master/hr > ~/bin/hr 
# or, in case curl is not installed
$ wget https://raw.github.com/LuRsT/hr/master/hr > ~/bin/hr

$ chmod +x ~/bin/hr
```

add that bin directory to your PATH (`echo $PATH`), and enjoy your hr time :)

### `ls` by modification date

List files in terminal sorted by modification date

    $ ls -lt

### Trash

Safer delete than `rm`. It permanently removes the files from the hard drive. We can make a safer way to delete files as first put them to trash.

    $ sudo apt-get install trash-cli

* trash-put
* trash-list
* trash-empty

    $ sudo nano -Y nanorc .bashrc

add line: 

    alias del="trash-put"

### Calculate disk usage

    $ du -h -d 1 --exclude="./.*"

`-h` human readable format
`-d` depth
`--exclude=’./.*’` exclude hidden directories

### Find

    $ find . -type f -name “*.xml” -print -exec grep -R “text to find” {} \;