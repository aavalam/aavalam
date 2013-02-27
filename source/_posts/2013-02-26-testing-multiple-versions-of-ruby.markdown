---
layout: post
title: "Testing multiple versions of Ruby"
author: Victor Goff
date: 2013-02-26 17:24
comments: true
categories: [Ruby, Testing, Versions] 
---
When you have code that you would like to test, it is fairly simple to
develop your tests to allow for it to be ran in more than one version of
Ruby. <!-- more -->

This is part of the code that I use through inspiration from the [Ruby Spec](https://github.com/rubyspec/rubyspec/blob/master/core/fixnum/bit_xor_spec.rb#L63) project.  I haven't checked the code, so I don't believe it is identical in functionality.

The helper.rb file is loaded with my helper file in my testing folder.

{% codeblock ruby_version_is - helper.rb %}
def ruby_version_is(version_string)
  if version_string == RUBY_VERSION
    block_given? ? yield : true 
  end
end
{% endcodeblock %}

This allows me to do the identical thing you saw on line 63 of that link
above.  In other words, I can use it with a block and it just does the
right thing.

Or I can use it like a query, and it will either return true or nil.

This makes it simple for me to have tests that are version specific, yet
won't fill my tests with failures just because of a version difference.

It also lets me search for those things that are specific to a version.

Ruby 2.0.0-p0 is out, and I used it to document the new to_h
functionality

{% codeblock Test using ruby_is_version - core_struct_to_h_spec.rb %}
require 'spec_helper'

Car = Struct.new(:make, :model, :year) do
  def build
  end
end

ruby_version_is '2.0.0' do
  describe 'Ruby 2.0.0 stuff' do

    before :each do
      @car = Car.new('Toyota', 'Prius', 2014)
    end

    it 'converts class to hash' do
      @car.to_h.must_equal make: 'Toyota', model: 'Prius', year: 2014
    end

  end

end
{% endcodeblock %}

Now I can run this test alongside others, and I don't have to worry
about what version of Ruby it is testing against.

I think that I will add some functionality though.  So I can specify a
minimum version of Ruby, and when 3.0.0 comes out, I will know what
things change based on the tests, because they will run against that
version as well, while not running against previous ones.

Anyway, how do you test against different versions of Ruby?

Continue this conversation on our [Google Plus post](https://plus.google.com/u/0/116568773932133159290/posts/Ffzy66e8TrH)!
