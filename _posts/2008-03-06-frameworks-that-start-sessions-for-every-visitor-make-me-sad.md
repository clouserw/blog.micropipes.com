---
layout: post
title: Frameworks that start sessions for every visitor make me sad
tags:
- Mozilla
---
I might have played the devil's advocate when [Lars][1] was hating on frameworks
at the [barcamp][2] last weekend, but that doesn't mean I don't see his point.
The latest in a series of frustrations with frameworks kept me up until 3am last
night.  What better way to cap it off than complaining on the internet?

Today's subject is anonymous sessions.  Frameworks (and developers) love them
because they are simple and convenient, but it comes at a cost.  Keeping track
of sessions for every visitor on a high traffic site is far too expensive to be
practical.  Developers should know how to work around this, but their frameworks
need to support them.

The first framework on my mind is [Drupal][3].  I filed [an issue][4] last year
that Drupal should support disabling anonymous sessions.  It's still unassigned
so I'm guessing it's not a high priority, but it was one of the main things that
made me choose not to use Drupal on mozilla.com.  I [wrote some ideas][5] on how
to handle it and got some responses from people suffering the same fate.  No
word on any progress though.

The second framework, [CakePHP][6], has an AUTO\_SESSION variable that, [just
like $cacheQueries][7], is far to easy to misplace faith in.

By setting AUTO\_SESSION to false, you can't read or write to the session.
Working as advertised?  Not so much.  If you take a closer look at what's
actually happening you'll see that the session is still getting started, it's
just that CakePHP is blocking your access to it.  Even with AUTO\_SESSION off, a
cookie with a unique ID is set, and <strong>a row is still inserted into the
sessions table</strong>.  That last part almost brought down [AMO][8] last
night.  I wrote [a patch that disables anonymous sessions for real][9], but
anyone that has talked to me about patching core code knows I don't like to do
it.

When you're writing code, framework or not, don't forget about scalability.

[1]: http://staff.osuosl.org/~lohnk/blog/
[2]: http://barcamp.org/BeaverBarCamp
[3]: http://drupal.org/
[4]: http://drupal.org/node/201122
[5]: http://drupal.org/node/183006
[6]: http://cakephp.org/
[7]: http://micropipes.com/blog/2008/01/07/cakephps-cache-that-wouldnt-quit/
[8]: https://addons.mozilla.org/
[9]: http://viewvc.svn.mozilla.org/vc/addons/trunk/site/cake/libs/controller/components/session.php?r1=10970&r2=10969&pathrev=10970
