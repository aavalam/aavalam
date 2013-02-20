---
layout: post
title: "Using RubyDocTest for development"
author: Victor Goff
date: 2008-09-07 02:10
comments: true
categories: [Test, TDD, Doctest, Ruby, Rubydoctest, Testing]
---

First of all, you must have installed rubydoctest which can be installed as a gem, or from source.  Source can be found here: [rubydoctest](http://rubyforge.org/projects/rubydoctest/) and the handy `gem install rubydoctest` can be used as well.

I just want to introduce you to the tool.  I find it handy when I want to verify things in irb, which I have open anyway, and it helps to document my code inline, or to have a .doctest file sitting next to my file (or in the ../tests directory) <!-- more -->

Of course, we are going to use a very contrived example.  I doubt anyone would code this way for such a simple solution (and a little bit not accurate in the calculations).  But it does show a few things about doctest.

We have covered shortly how to acquire rubydoctest.  Now let's talk about using it.  There are two ways to use it.  Internal to your code, and external as a .doctest document.  We will be using it in line with our code.

Our code problem will be this:  How many minutes are in a year.

What we are going to do, just for this exercise, is setup a hash, like this:

``` ruby minutes_in_year.rb
#!/usr/bin/ruby
# Write a program that will give you minutes in a year.

leap = false
TimeUnits = {:seconds => 60, :minutes => 60, :hours => 24, :days => (leap ? 30.5 : 30.4167), :months => 12}
```
(I warned you this was contrived!)  Obviously the first couple of things we want to confirm is that leapyear indeed affects the assignment of your constant TimeUnits value of :days.

We can do this in IRB: (and it may be that we were playing in IRB first, testing other ideas, before we came up with this, which will be the start of our program!)

``` ruby IRB Session
>> leap = false
=> false
>> TimeUnits = {:seconds => 60, :minutes => 60,   :hours => 24,
?> :days => (leap ? 30.5 : 30.4167), :months => 12}
=> {:minutes=>60, :hours=>24, :days=>30.4167, :months=>12, :seconds=>60}
>>
```

And as you can see, we now have the makings of our first doctest.  But it also brings up the question of "How?"

So, a little explanation; DocTests are comments inside your code that you create to give a test name, and the results of any tests, as they are expected to be.  So, here is the format to create what we have above... (I use multi-line comments in block format (=begin, =end), you can use the hash comment style if you like).  So below my code, I place the following lines:

``` ruby minutes_in_year.rb
>> leap = false
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167)})
=> {:minutes=>60, :hours=>24, :days=>30.4167, :months=>12, :seconds=>60}
```

You can see that this is the exact same output from IRB if you use the `irb --simple-prompt` command at your console.  As easy as copy/paste to get your tests and assertions, and I consider this a BIG plus!

However... we are not ready to test yet.  Remember I stated that doctests are comments.  This is not a comment... so we have some setup work to do... simply we will start our comment block, above the lines shown, and name our test.  It looks like this:

``` ruby minutes_in_year.rb
=begin 
doctest: Setup Time Units values in hash (not leap year)
>> leap = false
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167)}) 
=> {:minutes=>60, :hours=>24, :days=>30.4167, :months=>12, :seconds=>60}
=end
```

Now we have a doctest with a test name of "Setup Time Units values in hash (not leap year).  The second line of test is  >> leap = false.  You can note that there is no 'results' line underneath.  This is because we don't actually want to test for a result... we just want to setup the state in IRB.  We are assuming that the assignment here will be successful.

Now it is time to test it.  How to do this?  We save the file, and (I will use `minutes_in_year.rb`) run `rubydoctest minutes_in_year.rb` like so:

``` text Command Line
c:>rubydoctest minutes_in_year.rb
=== Testing 'minutes_in_year.rb'...
OK  | Setup Time Units values in hash (not leap year)
1 comparisons, 1 doctests, 0 failures, 0 errors
```

If you are in windows,  you may not see the color, but the OK here is green.  (In the final view of the file, you will see how I get color...  but that is mentioned in another blog post here.)  In any case... we now have the beginning of our program, complete with a test.  If we were to refactor later, obviously, we would likely need to change our test (It won't fail, due to being self contained...) but it will remind is via documentation what we were doing when we come back and look at it.  

On to the next portion of our program.

We want to make sure that our hash is working with the ternary operator, so we type and see the following in IRB:

``` ruby IRB Session
>> TimeUnits[:days]
=> 30.4167
```

And we see it is good, so we can add it to our doctest area.

Hint:  You may be asking "Why am I testing such a simple thing?"  Extra credit for you if you do this exercise and use merge method, rather than merge! method... If you did not use this test, you would not catch that bug.

But we also want to check if it is working for leap = true.  We must setup the constant TimeUnits again...

``` ruby IRB Session
=begin
doctest: Test our leap year true case for TimeUnits
>> leap = true
=> true
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167) } )
=> {:months=>12, :days=>30.5, :minutes=>60, :hours=>24, :seconds=>60}
>> TimeUnits[:days]
=end
```

Which we have confirmed, so we can place the lines into our doctest comments.

We haven't changed our code at all, yet, right now, just documenting what we want it to do based on different conditions.

So, let's think in IRB about how we are going to calculate minutes in a year. 

I end up doing this:

``` ruby IRB Session
>> leap = false => false
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167)})
=> {:months=>12, :days=>30.4167, :minutes=>60, :hours=>24, :seconds=>60}
>> x = 1
=> 1
>> TimeUnits.each_pair {|key, value| x = x * value unless key ==
>> :seconds}
=> {:months=>12, :days=>30.4167, :minutes=>60, :hours=>24, :seconds=>60}
>> x => 525600.576
```

And everything looks 'ok' to me.  I am sure the result is not totally accurate... but good enough for me...

It goes into my doctest as well, and then the code goes into my program...   I will call the test as follows:

``` ruby minutes_in_year.rb
doctest: Setup for minutes in non-leapyaer
>> leap = false
=> false
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167)})
=> {:months=>12, :days=>30.4167, :minutes=>60, :hours=>24, :seconds=>60}
doctest: compute minutes in a non-leapyear
>> x = 1
=> 1
>> TimeUnits.each_pair {|key, value| x = x * value unless key ==
>> :seconds}
=> {:months=>12, :days=>30.4167, :minutes=>60, :hours=>24, :seconds=>60}
>> x
=> 525600.576
```

And hopefully if I have done everything right, with my notes, and such, you should end up with a rubydoctest that ends up something like this:

``` text Console
=== Testing 'minutes_in_year.rb'...
OK  | Setup Time Units values in hash (not leap year)
OK  | Test our leap year true case for TimeUnits
OK  | Setup for minutes in non-leapyaer
OK  | compute minutes in a non-leapyear
9 comparisons, 4 doctests, 0 failures, 0 errors
```

Perhaps this is almost the code you ended up with...

``` ruby minutes_in_year.rb
#!/usr/bin/ruby
# Write a program that will give you minutes in a year.

leap = false
TimeUnits = {:seconds => 60, :minutes => 60,   :hours => 24,
  :days => (leap ? 30.5 : 30.4167), :months => 12}
  
=begin 
doctest: Setup Time Units values in hash (not leap year)
>> leap = false
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167)}) 
=> {:minutes=>60, :hours=>24, :days=>30.4167, :months=>12, :seconds=>60}
=end

=begin
doctest: Test our leap year true case for TimeUnits
>> leap = true
=> true
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167) } )
=> {:months=>12, :days=>30.5, :minutes=>60, :hours=>24, :seconds=>60}
>> TimeUnits[:days]
=end

# some additional notes:  doctests can contain comments like this inside, 
# for further documenting thoughts.
# I chose not to do this.
# Also, as you can see below, doctests don't have to be seperated as above,
# they could be as below.  
=begin
doctest: Setup for minutes in non-leapyaer
>> leap = false
=> false
>> TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167)})
=> {:months=>12, :days=>30.4167, :minutes=>60, :hours=>24, :seconds=>60}
doctest: compute minutes in a non-leapyear
>> x = 1
=> 1
>> TimeUnits.each_pair {|key, value| x = x * value unless key ==
>> :seconds}
=> {:months=>12, :days=>30.4167, :minutes=>60, :hours=>24, :seconds=>60}
>> x
=> 525600.576
=end

leap = false
TimeUnits.merge!( {:days => (leap ? 30.5 : 30.4167)})
x = 1
TimeUnits.each_pair {|key, value| x = x * value unless key == :seconds}
puts x

# Another time, perhaps, we can explore this in a more robust area, or 
# cover some other things.
```
