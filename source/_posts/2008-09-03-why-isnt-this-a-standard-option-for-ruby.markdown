---
layout: post
title: "Why isn't this a standard option for Ruby?"
author: Victor Goff
date: 2008-09-03 13:16
comments: true
categories: [Ruby, Prompt] 
---

Hints for use:
``` ruby simple useage
name = 'Please enter your name'.prompt
```
I know that each time I want to ask a user for something, I need to
write a way to ensure that the user sees the prompt, so that an
appropriate answer can be provided.  <!-- more -->It makes sense to provide a method
to do this, as it seems to be a pretty routine thing.

I do this by extending String with method prompt.  It is easy to use,
and ensures that stdout is flushed so that the user will get the
question.  If you find it useful, feel free to use it!

Maybe the method will be included some day as a core feature!

``` ruby prompt.rb
class String
  def prompt
    print self
    STDOUT.flush unless STDOUT.sync
    gets
  end
end
```
