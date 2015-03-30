---
layout: post
title: Micro blogpost remap  jj to escape
---

I want to move as quick as possible in Vim. Reaching for the escape key is a drag and makes me move my fingers of the home row.

## Challenge accepted
Let us move remap the escape-key to `jj`.

```vim
inoremap jj <esc>
```
Done!

### But wait there is more!

Of course this already works but it does not force us to actually use `jj`.
How could we force ourselves to use `jj` and make it a pain to use escape?
Let us map escape to escape and echo a message. 
This will let us use escape as normal but will flash a message at the bottom making it an annoyance to use.

``` vim
inoremap <esc>  <esc>:echom ">>> Okay, I'll escape for your this time. <<<"<CR>
inoremap jj <esc>
```

And that's it for this short blog post on vim and remapping the escape key :)

