---
layout: post
title: "Fuzzy Equality in RubyDocTest"
author: Victor Goff
date: 2008-09-11 1:00
comments: true
categories: [Fuzzy, Equality, Testing, Rubydoctest, Ruby, Doctest]
---
I was working on some tests for a standard exercise with temperature conversion. I then realized that there was no provision for testing if something is equal to a certain precision. As happens with different math problems concerning Float, different actions and different processors can give different answers. It doesn't matter to me in this instance, as long as it is within a 'tolerance'.<!-- more -->

So, I hopped into my favorite editor, to quickly write some code to generate some ranges of acceptable answers for my method.

I wanted my method to respond with numbers that aren't formatted to any precision, just native floating point numbers, but as this is an exercise that students are going to write, it is common for some of them to return answers that are 'correct' to the 10ths place, or 100ths place.

I want to be able to check the work semi-automatically, and so I used this for my doctest:

``` ruby IRB Session
>> ((37.74)..(37.8155555555556)) === convert(100.0)
=> true
>> ((-17.205)..(-17.2394444444444)) === convert(1.0)
=> true
```

And it works well... I can now use any student supplied method, and find out if their math is 'close'. But, now I can do it from different locations, so if I am working on an older system with a floating point error, my tests should pass, even if the results aren't exactly on.
