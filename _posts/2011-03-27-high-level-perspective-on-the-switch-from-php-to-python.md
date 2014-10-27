---
layout: post
title: High level perspective on the switch from PHP to Python
tags:
- Mozilla
---
<em>It may be fatuous to write this post before we've actually finished the
transition from PHP to Python, but I started writing a different post and this
is what came out.  Sometimes that happens.</em>

In January of 2010 we started migrating [addons.mozilla.org][1] from CakePHP to
Django.  It was a controversial decision.  Developers were ambivalent to
excited, managers were opposed to neutral - a split anyone would expect.  When I
[first talked about it][2] I expected to be able to turn off PHP by the end of
the year.  It didn't turn out quite like that.

Fifteen months later we're still transitioning and it's still stressful.  The
toughest part about a major migration like this is that there is only one team
that is doing the migration, continuing to add the new features we need, and all
the while maintaining the old site.  That's a stressful environment for
developers since the interactions between the languages can be complicated, it's
stressful for managers because features take longer to complete, and it's
stressful for users (and QA for that matter) because issues <em>will</em> arise
which are hard to reproduce and complicated to explain.

In the midst of all the work of migration, the rest of the company is still
working:  the security team is [announcing bounties on our site][3] which means
we need to be vigilant about fixing issues, project management continues to come
up with features to be added, the site perseveres in its never-ending quest for
a new <em>look and feel</em>, and [Firefox 4 is using AMO like never before][4]
meaning approaching 10,000 hits per second is a regular day.  All of that is
specific to the add-ons site, but consider your own company if you're thinking
of going down the same road - what is coming up for your site that will throw a
wrench in the works?

The meat and potatoes of it really comes down to:  Given the hindsight of today,
would the migration be a good idea?  There isn't a right answer for every site,
but for AMO we did the right thing[1].  As of today the majority of pages that
matter are on Python - there are some admin tools, and some cron jobs, and the
occasional semi-obsolete public page that is on PHP, but for the most part,
we're looking really good ([less hand waving, more real data][5]).  My new
(overly optimistic?) plan is to have PHP off by the end of <em>this</em> year.
We'll see.

To give you an idea of man-hours, we've had anywhere from 3 to 6 superhero
developers working on the site over the past 15 months, and it's looking like
the whole thing will take around 24 months.  That's a big chunk of time for a
site that needs to grow and evolve as quickly as popular sites do these
days.

So, overall, I think the lesson is: any reasonably sized site is going to have
rabbit holes in it.  At first glance AMO might look like it's got a dozen "main"
pages, with a couple dozen more supporting pages (and throw in a few more for
the admin CRUD).  Have a look at that spreadsheet I linked above and you'll see
that's not even remotely the case.  The spreadsheet even ignores sub-pages in a
few places and doesn't include any new features added in the past year.  If
you're considering a migration, think it through well.  Make a spreadsheet of
every URL, identify the complicated areas, and make sure everyone is clear on
the timeline and what it means for new features.  People will absolutely try to
scope creep your migration - make it clear if a section of the site is migrating
as-is or can be migrated and redesigned at the same time.  Redesigns add
complexity for the developers but can earn you some good will with the users and
managers and if you're in this boat you can use all the good will you can get.

May you have the best of luck with your decisions. :)

[1] I'll write another post about pros/cons of the actual frameworks and
platforms.  Let's just assume we're happy with the technical side of the switch
for now.

[1]: https://addons.mozilla.org
[2]: /blog/2009/11/17/amo-development-changes-in-2010/
[3]: http://blog.mozilla.com/security/2010/12/14/adding-web-applications-to-the-security-bug-bounty-program/
[4]: http://blog.mozilla.com/addons/2011/03/22/firefox-4-add-ons/
[5]: https://spreadsheets.google.com/ccc?key=0AgX-nlaDaTaBdGhVd3ZlU1ZySWRiNmZ4YmgxTkV6ZlE&hl=en
