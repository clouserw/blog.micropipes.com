---
layout: post
title: PHP is dead!  (on addons.mozilla.org)
tags:
- Mozilla
---
This is just a short note to recognize the long coming milestone of PHP being
effectively off[1] on addons.mozilla.org.  We [started the migration][0] in
2010 and just finished it up a couple weeks ago.  After the major pages were
completed it was hard to budget time for all the minor details we had
implemented since there was so much other important stuff to do (I'm looking at
you, marketplace.mozilla.org).  Now that the switch is done though we can
simplify our setup instructions for AMO, simplify our infrastructure, optimize
apache for python only, have full unit test coverage - the list goes on.

A big thanks to all the developers who made the switch possible, and especially
the ones at the end who were working on migrating PHP scripts instead of more
glorious projects.  Thanks to the management and all the other folks affected by
the switch for being patient with the scheduling.  Thanks to the localizers for
dealing with the crazy merged .po files, and, of course, thanks to the users of
AMO for reporting bugs when they happened and generally being an all around
great community to work with.

[1] Currently all traffic is being rewritten to a WSGI handler for Python.  PHP
is still on the server but nothing uses it.  We'll be removing it completely in
the near future.

[0]: /blog/2009/11/17/amo-development-changes-in-2010/
