---
title: Lua
subsection: lua
section: tech-languages
order: 1
version: 5.4.3
description:  Lua is a powerful, efficient, lightweight, embeddable scripting language.
---

# About Lua

[Lua](https://www.lua.org) is powerful, lightweight interpreted scripting language with a small footprint. It supports multi-paradigm programming: procedural, object-oriented, functional, data-driven and data-description. Lua is rarely used as a stand-alone language. Instead Lua focuses on scripting, as "secondary" language which integrated into other software written in mainly C/C++. 

Some examples of Lua's usage areas: network software, video games, user graphical interfaces, graphics/text processing software, etc. Lua also is good for beginners to create simple video games.

Lua interpreter is written in ANSI C and it is extremely small, both interpreter and source code is only about 1Mb. Lua is considered one of the fastest interpreted languages.


## Checking Lua

Some distributions already have Lua pre-installed. Open your terminal and type:

```bash
lua
```

If the output is be something like:

```bash
Lua 5.4.3  Copyright (C) 1994-2021 Lua.org, PUC-Rio
>
```

Congratulations! Lua is already installed on your system and ready to use.

<ins>Hint!</ins> To exit Lua's interpreter press <kbd>Ctrl + D</kbd>.

## Lua installation

If you see the message:

```bash
bash: lua: command not found
```

It means that Lua is not installed yet. The simplest way to install Lua from package manager `dnf`, which comes with Fedora. In your terminal type command:
```bash
$ sudo dnf install lua
```

Congratulations! Lua interpreter is installed!

## Lua syntax

Lua's syntax is very similar to languages Python, Ruby and C. For details check [official Lua manual](https://www.lua.org/manual/5.4/manual.html).

### Learning Lua

Lua is very fun and simple to learn, but hard to master. Here is an example of classical _hello world_ program:

```lua
print("Hello, world!")
```

Example of the program to calculate factorial, from the book [Programming in Lua](https://www.lua.org/pil/1.html).

```lua
function fact (n)
  if n == 0 then
    return 1
  else
    return n * fact(n-1)
  end
end

print("enter a number:")
a = io.read("*n") -- read a number
print(fact(a))
```

