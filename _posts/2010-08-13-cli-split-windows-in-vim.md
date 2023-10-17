---
layout: post
title: CLI Split Windows in Vim
tags:
- Mozilla
---
I use split windows, both horizontally and vertically, in [Vim][1] all the time.
I've always wanted to be able to split the window and then start a command line
shell within that window but up until now that has just been a dream.

[My friend][2] sent me a link to [conque][3] this morning which I'm so taken
with that it's prompted me to drop coding and write a blog post.

Conque lets me do exactly what I've wanted, create shells within Vim.  In insert
mode you interact with the shell as expected.  In normal mode you can scroll
back through your history, yank text into buffers, paste and manipulate text.
Best thing ever.

<a href="{{ site.baseurl }}/assets/img/vim_cli.png"><img src="{{ site.baseurl }}/assets/img/vim_cli_small.png" /></a><br />
<caption>Two files open on the left, three shells on the right; iPython, MySQL, and Django's web server - all with syntax highlighting.</caption>

[1]: http://www.vim.org/
[2]: http://hopson.ws/blog/
[3]: http://code.google.com/p/conque/
