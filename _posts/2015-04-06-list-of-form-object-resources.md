---
layout: post
title: A list of form object resources
---

The last year or so I have really become a fan of form objects and writing plain ruby objects (PORO).
I gathered some resources on how other people use these. This might help if you want to use form objects but are not sure where to start.

### Resources

1. [Upcase: Weekly Iteration Form Objects](https://upcase.com/videos/form_objects)

    Upcase has an excellent weekly iteration video showing how to use form objects.
    Unfortunately you'll need to pay for this one.

2. [Codeclimate: 7 ways to decompose fat activerecord models](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/)

    Apart from number 3. Extract form Objects. The other 6 points are great ways to keep your code clean.

3. [Github: HappyHours repo] (https://github.com/DefactoSoftware/Hours/commit/19633cced1fff71c58d914c01897b54610291ab4)

    [jurre] (https://github.com/jurre) made a pull request after watching the Upcase video. Check it out!
    I'm not a fan of the ```validate_children``` method since it keeps the validations in the model. One benefit of having the form object handle the validations is that the conditional validations are much easier to implement. I'll write up an example of how I use these another time :)

4. [Gem reform] (https://github.com/apotonick/reform)

    A wonderful gem that you really should check out before you are starting with form objects.

5. [Gem virtus] (http://davidmles.com/blog/2014/05/19/ruby-on-rails-patterns/)

    A blog post David morales about patterns which also mentions form objects using Virtus.

The gems reform and virtus handle a lot of configuration and allow you to hit the ground running. But they also add 'magic' which I try to avoid. I would say first try to write it yourself and grab a gem if it gets too hard.

This is a bare minimum but you should be able to set up your own form objects in your Rails app :)
Got any questions or have some tips hit me up on GitHub by creating an issue in my [github pages repo](https://github.com/sajoku/sajoku.github.io/issues/new)
