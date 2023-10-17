---
layout: post
title: AMO brings new levels of pedantry to Mozilla Webdev
tags:
- Mozilla
---

And we love it. :)

When we first started writing [AMO][1] in PHP we agreed to follow the [PEAR
coding standards][2] and left it at that.  Four years and thousands of lines of
code later it's roughly true, but there are some obvious mistakes and
oversights.  The main problem is that there is no automation for accountability.
If someone happens to see something out of line in a code review, they'll point
it out, but after a while everything starts to look the same.  Is that brace in
the right place?  Is there supposed to be a space there?  Minor stuff slips by,
it's not a big deal.

When we moved to python we needed a new style.  [PEP 8][3] is the obvious one
everyone goes with and we agreed we should follow it too.  Then [Jeff Balogh][4]
showed us a [check script][5] he wrote that automatically verifies code against
PEP 8, [PyFlakes][6], and complains if any lines are over 80 characters.  With
an automated system there is easy accountability and by checking it before you
commit it's easy to stay in line.

It's not a big deal if there are spaces around your equals signs, or if there
are two lines above your class declarations, but after thousands of lines of
code it can make scanning and finding what you want a lot easier.  The 80
character line limit is a classic programmer holy war and I think we settled on
a good compromise:  actual code is limited to 80 characters, templates can be
more but should be a "reasonable" length.  I took a screenshot of my actual
workspace one day as I was digging into some code.

<a href="{{ site.baseurl }}/assets/img/code_layout.png"><img src="{{ site.baseurl }}/assets/img/code_layout_small.png" title="IDE Screenshot" /></a>
<caption>Click to enlarge</caption>

What do you notice about style?  Aside from the Django code in the small window
closest to the center, all the files fit on the screen without ugly line
wrapping making it (relatively) easy to look at the full scope of <abbr
title="Model View Controller">MVC</abbr> flow, along with the unit tests and
some reference files.  Open up any of [our PHP files][7] and try that and it'll
just be a mess of wrapped lines or horizontal scrolling.

Code standards checks aren't something we took very seriously before but so far
I'm really happy with what we've got in AMO.  Automation makes all the
difference.

PS: I don't have to worry about blocking out any code in screenshots - isn't
open source great?  Sometimes people complain about not being able to share
their code and it always sounds so alien to me.  I don't usually advertise on
here, but if you want to share your code, [we're always hiring][8].

[1]: https://addons.mozilla.org/
[2]: http://pear.php.net/manual/en/standards.php
[3]: http://www.python.org/dev/peps/pep-0008/
[4]: http://blog.jeffbalogh.org/
[5]: http://github.com/jbalogh/check
[6]: https://launchpad.net/pyflakes
[7]: http://viewvc.svn.mozilla.org/vc/addons/trunk/site/app/
[8]: http://www.mozilla.com/en-US/careers/
