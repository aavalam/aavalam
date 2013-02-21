---
layout: post
title: "Using String's strip method rather than chomp"
author: Victor Goff
date: 2010-07-11 15:33
comments: true
categories: [String, Chomp, Strip]
---
I have been in the habit of using `String#chomp` when interactively
requesting input from people. I am considering using `String#strip`
instead. <!-- more -->It does more than `chomp`, in that it will remove leading
whitespace, trailing whitespace and still the `$/` which is to say the
record separator. I think that it is more suitable for interactive
input, unless you are counting on leading whitespace from someone for
some reason.

The statement that we always say when talking about `chomp` and `to_i` or
`to_f` is that `to_i` and `to_f` does the same thing as `chomp`, and this is
almost true. But `to_i` and `to_f` actually work more like strip.

Consider this:

``` ruby IRB Session
>> gets.strip
   98
=> "98"
>> gets.to_i
   98
=> 98
```
As you can see, in reality `to_i` strips the leading whitespace, and by
definition any trailing whitespace (though in reality all string content
that isn’t part of the first recognizable ‘numeric-like’ string)
including the record separator.

So, I am trading in my habitual `String#chomp` use for the cleaner
`String#strip` use, and where appropriate `String#strip!` and I believe I
will still have fun with Ruby!

Let me know what you think about this small movement?

