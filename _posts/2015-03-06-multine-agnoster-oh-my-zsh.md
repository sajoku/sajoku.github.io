---
layout: post
title: Make the oh-my-zsh theme agnoster multiline
---

I'm a big fan of
<a href="https://github.com/robbyrussell/oh-my-zsh" target="_blank">oh-my-zsh</a>
and in particular of the
<a href="https://gist.github.com/agnoster/3712874" target="_blank"> agnoster</a> theme you can install.

The regular setup is single line and looks something like this:
![agnoster regular]({{ site.baseurl }}/images/agnoster-regular.png "Agnoster regular")

My own setup looks more like this:
![agnoster multiline]({{ site.baseurl }}/images/agnoster-sajoku.png "Agnoster multiline")

I like to use a larger font and split my screens. My screensize is somewhat smalls (MacBook Pro 13 inch from 2011). So I decided I should make agnoster multiline which gives me back some of my screen real estate ;)

This is the code I used to make agnoster multiline.

{% highlight bash %}
prompt_newline() {
  if [[ -n $CURRENT_BG ]]; then
    echo -n "\%{\%k\%F{$CURRENT_BG}\%}$SEGMENT_SEPARATOR
\%{\%k\%F{blue}\%}$SEGMENT_SEPARATOR"
  else
    echo -n "\%{\%k\%}"
  fi

  echo -n "\%{\%f\%}"
  CURRENT_BG=''
}
{% endhighlight%}
(Note: remove the backslashes ```\``` when copying this in. Or get it from my github page
<a href="https://github.com/sajoku/dotfiles/blob/master/themes/agnoster.zsh-theme">github</a>)

The code above creates the arrow like seperator after which you can start typing your terminal commands.

Now we only need to add this newline funtction to the one that combines all the functions.

{% highlight bash %}
## Main prompt
build_prompt() {
  RETVAL=$?
  prompt_status
  prompt_virtualenv
  prompt_context
  prompt_dir
  prompt_git
  prompt_hg
  prompt_newline
  prompt_end
}
{% endhighlight %}


Now your terminal should look more like this.

![agnoster multiline]({{ site.baseurl }}/images/agnoster-sajoku.png "Agnoster multiline")


Hope you enjoyed this post :smile:
