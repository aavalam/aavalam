---
layout: post
title: "Understanding Modulo"
author: Victor Goff
date: 2008-09-08 22:11
comments: true
categories: [Ruby, Modulo, '%']
---
I can't think of a person that isn't aware of modular counting.  We do it just about every day... well, hopefully not while we are on vacation.  But every time you look at your watch, and figure out how many hours you have left before your work day is over, and it is before noon, you do it.<!-- more -->  Every time you have to time your goodies in the oven, or on the stove, you probably have to figure out some time past the top of the hour.  Microwaves even make us do it... the kids like corn dogs (are they dorkfish?), and the directions state 70 seconds for the first one, and 40 seconds for each additional.  So, they have to figure out the time in number of minutes and seconds... This is called modular counting.

I will place a table of calculations here that hopefully help to understand how Ruby uses the '%' method for class Fixnum.  The setup:  x is a time given in 24 hour time.  We only have a 12 hour clock on our wall... We want to know what the 12 hour time is.  The twist?  I will show you what it looks like when you have a negative 12 clock, or a negative time given, and I will show both.  It gives us four options for the format of "x mod 12" in the way of positive or negative values.

The way to think of this is look at the clock.  If x is positive, then you go around clockwise, like you are used to doing.  When it is negative, then you go to the left.  But, if the clock is negative, then all times are negative.  But, the x being the hand still rotates the way as just described, either counterclockwise if negative, or clockwise if positive.

Oh, in my table, I made one minor adjustment... Because it is a clock, I did account for 12 noon... Otherwise you would end up with 0 hour in the middle of the table... and we all know that midnight is 0 hour, noon is the 12th hour.  It also solves having a negative 0 in my table which was ruining the clock analogy for this explanation.

``` text Table
 x mod Time  |  x mod Time  |  x mod Time  |  x mod Time   
  0  12   0  |   0  12   0  |   0 -12   0  |   0 -12   0
  1  12   1  |  -1  12  11  |   1 -12 -11  |  -1 -12  -1
  2  12   2  |  -2  12  10  |   2 -12 -10  |  -2 -12  -2
  3  12   3  |  -3  12   9  |   3 -12  -9  |  -3 -12  -3
  4  12   4  |  -4  12   8  |   4 -12  -8  |  -4 -12  -4
  5  12   5  |  -5  12   7  |   5 -12  -7  |  -5 -12  -5
  6  12   6  |  -6  12   6  |   6 -12  -6  |  -6 -12  -6
  7  12   7  |  -7  12   5  |   7 -12  -5  |  -7 -12  -7
  8  12   8  |  -8  12   4  |   8 -12  -4  |  -8 -12  -8
  9  12   9  |  -9  12   3  |   9 -12  -3  |  -9 -12  -9
 10  12  10  | -10  12   2  |  10 -12  -2  | -10 -12 -10
 11  12  11  | -11  12   1  |  11 -12  -1  | -11 -12 -11
 12  12   0  | -12  12   0  |  12 -12 -12  | -12 -12 -12
 13  12   1  | -13  12  11  |  13 -12 -11  | -13 -12  -1
 14  12   2  | -14  12  10  |  14 -12 -10  | -14 -12  -2
 15  12   3  | -15  12   9  |  15 -12  -9  | -15 -12  -3
 16  12   4  | -16  12   8  |  16 -12  -8  | -16 -12  -4
 17  12   5  | -17  12   7  |  17 -12  -7  | -17 -12  -5
 18  12   6  | -18  12   6  |  18 -12  -6  | -18 -12  -6
 19  12   7  | -19  12   5  |  19 -12  -5  | -19 -12  -7
 20  12   8  | -20  12   4  |  20 -12  -4  | -20 -12  -8
 21  12   9  | -21  12   3  |  21 -12  -3  | -21 -12  -9
 22  12  10  | -22  12   2  |  22 -12  -2  | -22 -12 -10
 23  12  11  | -23  12   1  |  23 -12  -1  | -23 -12 -11
 24  12   0  | -24  12   0  |  24 -12   0  | -24 -12   0
```

