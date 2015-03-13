---
layout: post
title: Highlight lines that are more than 80 characters
---

When I code, mostly in Ruby but always in vim, I tend to follow the thoughbot
<a href="https://github.com/thoughtbot/guides/tree/master/style">styleguide</a>.
One _rule_ is _Break long lines after 80 characters._
Keeping track of the 80 character limit requires me to think about it, which causes me to lose focus.


Sometimes I decide to break the 80 character rule (guide ?) because the line is more descriptive if I make it 85 characters long. (I prefer descriptive methods above length rules, sue me!). This is where my bit of Vim magic comes in. This vim configuration highlights all lines when they cross 80 characters but first warns when you get near the set limit.

{% highlight ruby %}

hi LineProximity ctermfg=white ctermbg=gray guifg=white guibg=#757160
hi LineOverflow  ctermfg=white ctermbg=red guifg=white guibg=#FF2270

autocmd BufEnter,VimEnter,FileType *.rb,*.coffee let w:m1=matchadd('LineProximity', '\%<85v.\%>80v', -1)
autocmd BufEnter,VimEnter,FileType *.rb,*.coffee let w:m2=matchadd('LineOverflow', '\%>84v.\+', -1)
autocmd BufEnter,VimEnter,FileType,VimEnter *.rb,*.coffee autocmd WinEnter *.rb,*.coffee let w:created=1
autocmd BufEnter,VimEnter,FileType,VimEnter *.rb,*.coffee let w:created=1

{% endhighlight%}

The first two lines declare how the highlight should look (LineProximity and LineOverflow). I'll get to that later.
The autocmd make sure when vim opens a buffer (or any of the other options) and it's a .rb (Ruby) or coffee file it checks the regex and decides if it should highlight a line.

{% highlight ruby %}
'\%<85v.\%>80v'
{% endhighlight%}
Checks for anything between 80 and 85 and marks it with a gray background. This is Proximity.

{% highlight ruby %}
'\%>84v.\+'
{% endhighlight%}
Anything after the 84th character will have a red background. This is LineOverflow.

Check out the gif below. Looks nice doesn't it? Depending on your colorscheme it makes the colors pop more.

![vim highlight after 80 characters]({{ site.baseurl }}/images/overlength.gif "Highlight ruby coffee files after 80 characters")

You can customize this by changing the file extensions or changing the character length.
Next up is making this into its own plugin with some smarter behaviour.

### How to use?
Pop the lines in your .vimrc and you're good to go.

Hope you enjoyed this post :smile:
