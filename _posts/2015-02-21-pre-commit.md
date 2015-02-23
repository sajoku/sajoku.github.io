---
layout: post
title: Pre-Commit awesomeness
---

For a while now I've been using a pre-commit hook which prevents me from committing debug type lines in various files. This has the benefit of my debugging code never ending up in production and breaking things because I missed it.

Example:

{% highlight ruby %}
descibe ApplicationController, focus: true do
  it 'tests something' do
  end
end
{% endhighlight %}

When trying to commit the above code an error will be given by the Git client I'm using. Stating that I need to resolve the error first.

![git commit error message, please dont use git commit but add a message, k thx bye!]({{ site.baseurl }}/images/danger_git_commit.png "Don't commit me")

### A cleaner git history

You probably have come across commits like "Remove binding.pry", "Remove console.log".
<a href="https://github.com/search?q=remove+binding.pry&ref=searchresults&type=Issues&utf8=✓" target="_blank">GitHub results for a search on "Remove binding.pry"</a>
This pre-commit hook prevents commits like these and keeps your history clean. It also has the benefit of making sure this doesn't end up in your production code and breaking your app because of a stupid mistake.

I'm now using this for ```console.log```, ```focus: true``` and ``` binding.pry``` statements in the various files they are usually used in. The pre-commit only checks for binding.pry in ```.rb``` files making the pre-commit check a bit faster :).


### Credits where credits are due
I wasn't the first person to come up with this and all credits go to <a href="https://github.com/twe4ked/git-pre-commit" target="_blank">twe4ked</a> for making this pre-commit. I'm sure the performance can be better but this gets the job done really well.

### Usage
I forked the repo and made a simple change, adding in a check for ```console.log```.
You can find it here [git-pre-commit](https://github.com/sajoku/git-pre-commit).
Place this in a directory of your liking and add it to the global git config with
```
git config --global init.templatedir '~/.git_template'
```
I placed the pre-commit in my dotfiles with the following structure:
```
dotfiles/git_template/hooks/pre-commit
```
After which I ran
```
git config --global init.templatedir '~/dotfiles/git_template'
```

Now go into your project and run ```git init``` this will put the pre-commit in your hooks directory of the project.
```
/project/.git/hooks
```

###Caveats

Make sure the pre-commit is an executable (chmod +x).

Make sure the pre-commit is added in the .git/hooks directory of the project you want to add it.

Any other issues, additions to pre-commit hook or have performance enhancements? I welcome a pull-request any day :)
