---
layout: post
title: "Replace emojis with :aliases: on IRC"
tags:
- Mozilla
---

I work with some cool cats who are on the cutting edge of hip new technologies
like emojis.  OS X shows the emojis correctly but if I'm using IRC over SSH
from Linux all I see are missing characters:

<img src="{{ site.baseurl }}/assets/img/2016-noemoji.png" title="Emojis don't show up for me in IRC." />

Are they ready to push the site?  I always just assume so, but before that comes
back to bite me I decided to write a quick script to replace emojis with their
text aliases:

<img src="{{ site.baseurl }}/assets/img/2016-emoji2alias.png" title="Emojis are replaced with aliases." />

On the left is their view, and on the right is my client that is still stuck in
two-thousand-late.

If you run weechat and would like to use the script:

1. Copy [emoji2alias.py][1] to *~/.weechat/python*
2. Run `/python load emoji2alias.py`

If you want it to load automatically:

1. `cd ~/.weechat/python/autoload`
2. `ln -s ../emoji2alias.py .`

[1]: https://github.com/clouserw/scripts/blob/master/emoji2alias.py
