---
layout: post
title: Retiring AMO's Landfill
tags:
- Mozilla
---
A few years ago we deployed [a landfill for AMO][0] - a place where people could
play around with the site without affecting our production install and
developers could easily get some data to import into their local development
environment.

I think the idea was sound (it was modeled after [Bugzilla's landfill][1]) and
it was moderately successful but it never grew like I had hoped and even after
being available for so long, it had very little usable data in it.  It could
help you get a site running, but if you wanted to, say, test pagination you'd
still need to create enough objects to actually have more than one page.

A broader and more scalable alternative is a script which can make as many or as
few objects in the database as you'd like.  Want 500 apps?  No problem.  Want
10000 apps in one category so you can test how categories scale?  Sure.  Want
those 10000 apps owned by a single user?  That should be as easy as running a
command line script.

That's the theory anyway.  The idea is being explored [on the wiki][2] for the
Marketplace (and AMO developers are also in the discussion).  If you're
interested in being involved or seeing our progress watch that wiki page or
join #marketplace on irc.mozilla.org.

[0]: /2011/03/29/welcome-to-the-landfill/
[1]: http://landfill.bugzilla.org/
[2]: https://wiki.mozilla.org/Marketplace/Fake_Data
