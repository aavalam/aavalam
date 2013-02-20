---
layout: post
title: "Colorizing your NT Console with Ruby"
author: Victor Goff
date: 2008-09-02 4:23
comments: true
categories: [NT, Color, Ruby] 
---

I found the following snippet ( edited by me, for changes I wanted...) Credits are in the code block.
<!-- more -->

``` ruby Colorization based on ANSI Terminal Codes
=begin rdoc
This extends string to allow colorization based on ANSI
terminal codes.  The following code actually came from
Dmytro Shteflyuk's blog linked at end of this blog
Thanks to one of his readers for expanding it even further!
Finally, here in the current incarnation on my machine.

Usage: 'String content'.color
colorize('string or text content', color_code)

To get color code table, you simply call method ansi_color_table
=end

begin
require 'Win32/Console/Ansi' if PLATFORM =~ /win32/
rescue LoadError
raise 'You must gem install win32console to use color on Windows Console.'
end

class String
 def red; colorize(self, "\e[1m\e[31m"); end
 def green; colorize(self, "\e[1m\e[32m"); end
 def dark_green; colorize(self, "\e[32m"); end
 def yellow; colorize(self, "\e[1m\e[33m"); end
 def yellow_on_black; colorize(self, "\e[1m\e[33m\e[40m"); end
 def yellow_on_drkred; colorize(self, "\e[1m\e[33m\e[41m"); end
 def blue; colorize(self, "\e[1m\e[34m"); end
 def dark_blue; colorize(self, "\e[34m"); end
 def pur; colorize(self, "\e[1m\e[35m"); end
 def colorize(text, color_code)
"#{color_code}#{text}\e[0m" end
end

def ansi_color_table
[0, 1, 4, 5, 7].each do |attr|
 puts '----------------------------------------------------------------'
 puts "ESC[#{attr};Foreground;Background"
 30.upto(37) do |fg|
   40.upto(47) do |bg|
     print "\033[#{attr};#{fg};#{bg}m #{fg};#{bg}  "
   end
 puts "\033[0m"
 end
end
return
end
```

I have placed this file in my [ruby installation directory]\lib\ruby\site_ruby\1.8\ directory so it can be used as a library.

`yellow_on_black` and `yellow_on_drkred` are on the list for showing how to create additional 'listed' colors.

Easily extended list, and many, many applications.

The side affect of installing win32console is the added benefit of RSpec and Ruby DocTest being able to show actual colors in the output while testing, too.

So, fun toy for color, yes... practical, definitely!

Information gathered from [this blog](http://kpumuk.info/ruby-on-rails/colorizing-console-ruby-script-output/trackback/)!

