---
layout: post
title: Load local .vimrc settings
intro: Some sweet vim config
---

### The Short version

In your `.vimrc` set the following lines.

```
if filereadable(expand(printf('%s/%s', getcwd(), '.vimrc')))
  exec printf('source %s/%s', getcwd(), '.vimrc')
endif
```

The `if filereadable` will check if a `.vimrc` is available when booting vim.
If not it will do nothing, but it won't nag about it.

If a `.vimrc` is present it will load it.
Now just create `.vimrc` in a location where you start vim and it loads up the configuration from that vimrc.

### Why?

I have been spending a lot of time in various programming languages and development environments. I always try to use vim for everything that I need to do.
For a couple of projects I've found that I need to do something different than what I use in all the other projects.

With the following additions the your (global) .vimrc you'll be able to load local vimrc's.

A project I'm working on is linting the code with `rubocop`. My default is [`standard`](https://github.com/testdouble/standard).
So in my (global) `.virmc` the linter for Ruby is defined as:

```
let g:ale_linters = {'ruby': ['standardrb']}
let g:ale_fixers = {'ruby': ['standardrb']}
```

In the projects folder the linter is defined as following:

```
let g:ale_linters = {'ruby': ['rubocop']}
let g:ale_fixers = {'ruby': ['rubocop']}
```

When starting vim within the projects root (where the .vimrc is located) it will override the
linter and fixer settings for Ruby.

For example in `~/work/your-ruby-project` create a `.vimrc` with the line `echo "this is awesome"`.
Now cd in `your-ruby-project` and start `vim`.
It should echo the "this is awesome" 🚀
