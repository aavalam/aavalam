---
layout: post
title: "Ruby 2.0.0-p0 Notes"
author: Victor Goff
date: 2013-02-25 03:39
comments: true
categories: [Ruby, 2.0.0, Notes]
---
I have been waiting for the 24th of February to see what would come of
the planned release date for Ruby 2.0.0-p0.

I wanted to apply my "Learn By Testing" repository on this new Ruby, and
am running into a few problems. <!-- more -->  The first was Bundler 1.3.0 needs to be
installed.  Simple enough to install.  Just go to the repository, clone
it,  select the tagged version, then install it locally as a gem.

Trying to use a Gemfile with Bundler though is giving me some errors.

See, I am using Guard and I wanted to add the `rb-inotify` gem to my
`Gemfile`.  But in doing so, I get this error:

```
~/.rvm/gems/ruby-2.0.0-p0/gems/bundler-1.3.0.pre.8/lib/bundler/lazy_specification.rb:74:in `method_missing': LazySpecification has not been materialized yet (calling :required_ruby_version []) (RuntimeError)
        from ~/.rvm/gems/ruby-2.0.0-p0/gems/bundler-1.3.0.pre.8/lib/bundler/match_platform.rb:11:in `match_platform'
        …
        from ~/.rvm/gems/ruby-2.0.0-p0/bin/ruby_noexec_wrapper:14:in `eval'
        from ~/.rvm/gems/ruby-2.0.0-p0/bin/ruby_noexec_wrapper:14:in `<main>'
```

The problem is that in my RVM I had a bundler 1.2 version installed in
the @global gemset.

Removing the global bundler, making sure that Bundler 1.3.0 was
installed, seems to have corrected the issues. 

Now on to write tests for Ruby 2.0 and absorb some knowledge while
recording what I have learned.

