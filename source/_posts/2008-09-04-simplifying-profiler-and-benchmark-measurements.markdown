---
layout: post
title: "Simplifying Profiler and Benchmark measurements"
author: Victor Goff
date: 2008-09-04 02:43
comments: true
categories: [benchmark, profiler, ruby, wrapper]
---

Performance should be pretty close to the end of the list of things to do when programming in Ruby.  Yes, it can be important to get the timing down on your code.  But this is after you verify that it is running as you need it to, and it is actually usable.<!-- more --> 

That being said, there are two tools that can give you some pretty nice information when you want to know how your code is performing.  It can even be nice to know what is being called.  This blog will assume you know what these are, as I don't want to describe what they do, or how to use them.  I simply want to show a away to simplify using these tools for when you may want to use them.

What I have done for my use is put together a small collection of tools I use occasionally.  One such tool is for Benchmark (in the standard library).  I put it in a file, like so... `../site_ruby/1.8/mytools.rb`, and you know the rest...

I can then send blocks of code that I may want some time information on...

`v_benchmark("Loop 1 million times") {1.upto(1000000) {do whatever here}}`

Or your more traditional block with do..end block, etc...

The same thing works for Profiler... 

It is used identically the same was as the `v_benchmark` sample above. 

Have fun with this, I know I have had hours of enjoyment with it... and hopefully you will too... (though hopefully not with just one run...)

There is so much you can do with it, I will leave experiments to you...

Here are the code blocks....

``` ruby my_tools.rb
require 'rubygems'
require 'profiler'
require 'benchmark'

=begin rdoc
Provide v_benchmark with a report description as a string, and a block.
=end

def v_benchmark(test_description, &block)
  Benchmark.bmbm(test_description.size) do |x|
    x.report("#{test_description}") {yield}
  end
end

=begin rdoc
v_profile will give you profile information.  Provide it with a
String argument and a block.  The String argument is used for labelling
the report.
=end

def v_profile (block_description, &block)
  puts "BEGIN: #{block_description} profile:"
  Profiler__::start_profile
    yield
  Profiler__::print_profile($stderr)
  puts "END: #{block_description} profile report."
end
```

