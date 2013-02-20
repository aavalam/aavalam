---
layout: post
title: Private easy git repositories using rails and gitlab
date: 2012-10-28 03:02
author: Victor Goff
comments: true
categories: [Git, Rails, Gitlab, gitolite] 
---
I have installed [gitlab](http://gitlabhq.com/) about 4 times over the last 24 hours.
<!-- more -->

First I started with an install from turnkey, so that I could look over a well thought out install.  And it was pretty simple aside from one timeout issue.  Easilly fixed once I looked through the configuration files.  It was running vesion 2.5.0, you can download a virtual machine install from www.turnkeylinux.org, search for gitlab, 

I then blew away the VM and installed it again and made some changes that I wanted to see, just to get a feel for how I could manipulate things and break them.  

Finally, the last time (and this screenshot) is from an install right from the gitlab instructions.  It was very straight forward, I did find one error in /home/git/.gitolite.rc which had a single quote in the wrong place, I replaced it with a slash to give it a glob pattern.  (I think it was the right thing to do).  If you are
curious, it is on line 22.

This is version 3.0.3 and pulled down from the stable branch.

{% img /images/2012/10/45405183-image.png 812 748 Screenshot of GITLAB Dashboard %}

From playing with it a little bit (and I found out from pushing the gitlab stable branch only) that gitlab expects and requires a master branch to be created and pushed up, otherwise it doesn't know to display even the only branch that is there.  So that took me a moment to realize.

Remove the master branch, and you will go back to the instruction page directing you to do a git config --global username and mail
standard things for git configuration as it pertains to your
settings.

If you are wanting to play with the demo, you can from the link above... or if you would like to play with it with your own account, you can right at [gitlab.com](gitlab.com) (I don't know why that domain isn't in your face when you go to their main web page.)  They are running, as of this post, version 2.9.1.

If you decide to install it or use it in the various ways that you are able to, let me know your results, how you are using it, and what you think about it.  Have you customized it?  Added a registration page, etc.?

