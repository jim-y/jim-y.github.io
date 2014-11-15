---
layout: post
title: Toggle Whitespace in Sublime Text 2
published: true
categories: [linux]
tags: [sublime,whitespace]
---

A simple way to create a shortcut for toggling show_white_spaces in Sublime Text 2. Credits [facelessuser](https://www.sublimetext.com/forum/viewtopic.php?f=3&t=6347#p27580)

# Installation

`Tools` -> `new Plugin`

```py
import sublime
import sublime_plugin


class ToggleWhiteSpaceCommand(sublime_plugin.ApplicationCommand):
    def run(self):
        settings = sublime.load_settings("Preferences.sublime-settings")
        white_space = "selection" if settings.get("draw_white_space", "selection") != "selection" else "all"
        settings.set("draw_white_space", white_space)
        sublime.save_settings("Preferences.sublime-settings")
```

Save as `toogle_white_space.py`, then open up User Key Bindings, by

`Preferences` -> `Key Bindings User`, and add this:

```json
[
  {
    "keys": ["ctrl+alt+w"], "command": "toggle_white_space"
  }
]
```

`ctrl+alt+w` is the same what i use in `WebStorm`.

Thats it, try out :)
