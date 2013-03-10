---
layout: post
title: "Ruby 2.0.0 Params Not Just for Methods"
author: Victor Goff
date: 2013-03-09 03:46
comments: true
categories: [Ruby, Params, Proc, Lambda]
---
While working on documenting things I learned through a Learn Ruby By
Testing project, I came across documenting the new Ruby 2.0 'Params'
feature.

I realized that Methods are blocks and Procs and lambdas are very
close, so was wondering if the arguments would cross over.

It turns out that it does.
<!-- more -->
If you are not familiar with the new "named parameters" feature, it
works by taking a Hash argument, along with another new syntax that
starts with a two asterisks.  Similar to the "optional argument" syntax,
it basically accepts all other non-named hash keys that you would give
your method.  Or, Proc or lambda.

Let's look at the signature:

{% codeblock ruby_two_oh_params.rb %}
def some_method(*args, name: 'Joe', age: 23, **additional_params)
{% endcodeblock %}

This describes an argument list consisting of an 0 or more arguments for
`*args`, a named parameter called name, with the value of 'Joe' by
default, and a named parameter of age, with a default value of 23, and
at the end, the syntax that allows you to pass in arbitrary number of
hash keys, with values.

It is important to note that in order to have the **additional_params at
the end, after the normal Hash that you may be used it, you must use the
Ruby 1.9 syntax of `key: value`, rather than `:key => value`or it will
break.

Well, that is wonderful, as it means that we no longer need to do the
hash merge to bring in default 'params'.

But you will have likely read about that elsewhere.

The thing that I was happy to discover was the "named params" are available
for Proc and lambda.

This means that we can now do something like this:

{% codeblock named_params_for_proc_and_lambda.rb %}
my_proc = Proc.new do |name: 'Joe', age: 23, **other_params|
  [name, age, other_params]
end
{% endcodeblock %}

If you were to pass nothing at all to the Proc, you would get this: `["Joe", 23, {}]`

Let's see what happens if you change the name, and give it a some
undetermined parameter:
{% codeblock example_use.rb %}
my_proc = Proc.new do |name: 'Joe', age: 42, **other_params|
  [name, age, other_params]
end

my_proc[age: 49, hobbies: ['long walks', 'candlelight dinners', 'romantic comedies']]
{% endcodeblock %}
We would end up with this as a return:

`["Joe", 49, {:hobbies=>["long walks", "candlelight dinners", "romantic comedies"]}]`

Compared to the extra work we would have had to do to get this in Ruby
1.9, I like it.

Did you know that the conversation starts here, but continues on in our [Google Plus+
Post](https://plus.google.com/u/0/116568773932133159290/posts/KJrYYhbMDLz)?

