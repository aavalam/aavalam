---
layout: post
title: "Improved Prompt method"
author: Victor Goff
date: 2008-09-04 02:03
comments: true
categories: [Prompt, Ruby]
---

Welcome to little random thoughts of Ruby... My topic tonight is about the prompt snippet I gave yesterday.  I didn't realize it, as often happens, but it was so simple, I had to add the feature.

I realized while writing another wrapper for benchmark and profiler, that it is pretty common to add chomp() to our gets.  But there may be times when we want what gets, um... well, gets.<!-- more -->  (Who am I to assume what you may want?)  So I give an option.  I default to a plain old string that is stripped.  But you can easily get the true gets result by asking for true results.  Can you guess that the flag to get it could be 'true'?

``` ruby improved_prompt.rb
class String
=begin rdoc
usage: variable = 'String to display'.prompt
then enter in the string you want to assign to variable.
Alternatively, you can provide a Press Any Key to Continue"
function.
=end
  def prompt(no_chomp = false)
    STDOUT.flush unless STDOUT.sync
    return gets.chomp unless no_chomp
    gets
  end
end
```

In my irb, Here are a couple of examples...
``` ruby IRB Session
>> 'Please type something: '.prompt
Please type something: Something
=> "Something"
>> 'Please type something (This will not be stripped): '.prompt(true)
Please type something (This will not be stripped): Something
=> "Something\n
```

Well, I thought it was pretty cool.
