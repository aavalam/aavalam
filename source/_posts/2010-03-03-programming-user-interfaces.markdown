---
layout: post
title: "Programming User Interfaces"
author: José Carlos Monteiro
date: 2010-07-20 1:31
comments: true
categories: [Guest Post, Programming, General]
---
(Original post date: 03/Mar/2010)

My way of programming the computer systems have been normal, albeit slower than the technology has evolved, I began by imperative programming applications in command line mode and have I kept more within the server components of the solutions that have developed or maintained.

However, every time I make a foray into programming mode applications GUI it always suffers from too much friction and impedance. And even when you reach the end, most often it does not end up being what you expected from the beginning.
<!-- more -->
Leaving aside the issues connected with NPP - Non-Programmers Programming - and with the usual challenges around the lineup - Software Craftsmanship - This article addresses two issues: why is it difficult for programmers to encode good user interfaces and a possible answer to minimize this impedance ( Paper Prototyping ).  

Firstly, I have learned that 80% (or more) of the value of an application is evaluated by the user on the user interface of this application.

Jeff Atwood in his article "The User Interface Is The Application", says that no matter how spectacular the architecture diagrams are that exist for an application, with respect to the user of that application, the user interface is the application. It is true that the task of building a good user interface is difficult but to be taken seriously you have to go beyond and build an impressive user interface.

And he even cites Yukihiro Matsumoto, creator of the Ruby language:

If you have a good interface on your system, and the budget of money and time, you can work on your system. If your system has bugs or is too slow, you can improve it. But if your system has a bad interface, you have basically nothing. It will not matter if it is the work of the highest craftsmanship on the inside. If your system has a bad interface, no one will use it. So the interface or surface of the system, whether to users or other machines, is very important.

The assumption that building a good user interface is difficult, is it reasonable to expect that any programmer with no training or experience in UI Design can build and maintain a good user interface?

Some responses also came from another article from Jeff Atwood, ["UI is Hard"](http://www.codinghorror.com/blog/2005/06/ui-is-hard.html), where he writes that in part are the developers themselves primarily to blame because - like me - most programmers begin to think in code and business logic rather than begin by thinking about the user interface. And that majority is represented in part on your comments to this article.

Other responses came from other similar articles, ["UI Design"](http://blogs.msdn.com/rick_schaut/archive/2004/04/02/106929.aspx) blog "Buggin' My Life Away" by Rick Schaut and ["Can Programmers Do Interaction Design?"](http://www.cooper.com/journal/2003/08/can_programmers_do_interaction.html) by Kim Goodwin of Cooper in the Journal.

What is Rick points out that when working on software for the user it doesn't matter if it is a web application or desktop, or add new features, the focus is in designing the user interface - first and foremost. And this is complicated because programmers are first used to implement efficient algorithms for common problems in computer science but not learned or have enough experience on how to design a good user interface. Secondly, most of the tools facilitates the rapid creation of user interfaces for most simple problems of usability , but they tend to fall short of what is needed also to facilitate the rapid creation of interfaces for a set of usage scenarios that are more complex.

In another interesting article, ["The Rise and Fall of Homo Logicus"](http://www.codinghorror.com/blog/2004/09/the-rise-and-fall-of-homo-logicus.html) by Jeff Atwood quotes an excerpt from the book _The Inmates Are Running the Asylum_ by Alan Cooper: There is a large impedance for a programmer to design an interface for the user. Because while most developers have a more forward-thinking knowledge about how everything works, most users have only a  thought turned to the success of a task. He ends the article saying that we must stop thinking like Homo Logicus and think more like Homo Sapiens.

The article by Kim said that instead of resulting in the lowest cost having the programmers design the user interface it has been the opposite: it is more inefficient, more costly and more likely to be a failure. And the failures is that it results in more programming, right?

So how to avoid the impedance between what the programmer is able to create and what the user is typically waiting for?

First, many articles recommend to start the development by creating the user interface even to the point (extreme and ironic) to appoint a methodology to be followed: FAD.

Secondly, the use of paper prototyping - what other benefits avoids many of the pitfalls in prototyping applications - due to better mitigate the risks normally inherent in having the feedback of the users only after laborious programming tasks

* Posted in: [doCoding](http://recortis.dowedo-it.com/index.php/archives/category/docoding/)
* Author: José Carlos Monteiro
