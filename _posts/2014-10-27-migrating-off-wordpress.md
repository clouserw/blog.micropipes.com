---
layout: post
title: Migrating off Wordpress
tags:
- Mozilla
---

This post is a celebration of finishing a migration off of Wordpress for this
site and on to flat files, built by Jekyll from Markdown files.  I'm definitely
looking forward to writing more Markdown and fewer HTML tags.

90% of the work was done by [jekyll-import][1] to roughly pull my wordpress data
into Markdown files, and then I spent a late night with Vim macros and sed to
massage it the way I wanted it.

If all I wanted to do was have my posts up, I'd be done, but having the option
to accept comments is important to me and I wasn't comfortable using a platform
like [Disqus][2] because I didn't want to force people to use a 3rd party.

Since my posts only average one or two comments I ended up using a slightly
modified [jekyll-static-comments][3] to simply put a form on the page and email
me any comments (effectively, a moderation queue).  If it's not spam, it's easy
to create a .comment file and it will appear on the site.

My original goal was to host this all on Github but they only allow a short list
of plugins and the commenting system isn't on there so I'll stick with my own
host for now.

Please let me know if you see anything broken.

[1]: http://jekyllrb.com/docs/migrations/
[2]: https://disqus.com/
[3]: https://github.com/mpalmer/jekyll-static-comments/
