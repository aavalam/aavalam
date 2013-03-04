---
layout: post
title: "My partial VIM configuration"
author: Victor Goff
date: 2013-03-03 21:54
comments: true
categories: [VIM, Configuration, Editor]
---
What do you use to configure your editor?

I am usually in VIM for my editor.  Not the graphical (gvim) version, the one
that runs in the terminal.

I also use [Carlhuda's Janus](https://github.com/carlhuda/janus) configuration.

But there are things that I change that are simply minor things.
<!-- more -->
To do this, according to the documentation for customization, I use
`~/.vimrc.after` and here are my settings.

These are miscelanious things that I wanted to have.  The relativenumber
setting seems to not be as persistent as I would like though.
{% codeblock My Post Janus VIM Config lang:vim .vimrc.after %}
set t_Co=256
set showcmd
set foldmethod=syntax
set wildmenu
set wildmode=list:longest
set virtualedit=all
set visualbell
set relativenumber
set wrap
set linebreak
set nolist
set textwidth=0
set wrapmargin=0
{% endcodeblock %}

An abbreviation that I use pretty often.
{% codeblock My Post Janus VIM Config lang:vim .vimrc.after %}
" rdt<space> does an autocompletion which gives me a rubydoctest
" comment block
iab rdt =begin<CR>doctest: <CR>>> <CR>=> <CR>=end<CR><Up><Up><Up>
{% endcodeblock %}


This next line clears the highlights that happen when you search.  For me, my leader is `,`.

{% codeblock My Post Janus VIM Config lang:vim .vimrc.after %}
nnoremap <leader><space> :noh<cr>
{% endcodeblock %}


Add this in here if you really want to be enforced not to use the
arrow keys.  Enable it for a few days and pretty soon you just don't
reach for the arrow keys until you really need them.
{% codeblock My Post Janus VIM Config lang:vim .vimrc.after %}
nnoremap <up> <nop>
nnoremap <down> <nop>
nnoremap <left> <nop>
nnoremap <right> <nop>
inoremap <up> <nop>
inoremap <down> <nop>
inoremap <left> <nop>
inoremap <right> <nop>
{% endcodeblock %}

Well, there you have it. Most of my configuration file that I have in
addtion to the Janus configuration.

What things do you have in your configuration that you really like to
have?  I am sure it is more exciting than mine!

The discussion starts here, but continues on this [Google+ Post](https://plus.google.com/u/0/116568773932133159290/posts/WhzgA38YcnB)!
