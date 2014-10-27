---
layout: post
title: 'Inception: projects within projects'
tags:
- Mozilla
---
When we converted addons.mozilla.org from PHP to Python I mentioned how
deceptively large (lines of code) the site had grown with so many views and
features.  We've since built marketplace.firefox.com on literally the same code
base (a decision I hoped to blog about some day, alas) and the line count
continues upwards.  The <abbr title="Model View Controller">MVC</abbr> paradigm
is one of the most common out there, easy to understand, and built in to our
frameworks so it was naturally a good choice.  However, as the site continues to
expand we've had to review what the best architecture for the code would be and
the main point that stands out is that our entire site and its services are a
monolithic blob of code.  Both sites, all of our <abbr title="Application
programming interface">APIs</abbr>, all of the PayPal code, the administrative
tools, the developer control panel, the reviewer queues, the list goes on - it's
all in one repository and changing one means potentially affecting all of them.

With big plans for 2013 and no signs of slowing our code expansion we've hit the
point where it makes more sense to break the site up into smaller projects.
We've already started with our <a
href="https://github.com/mozilla/solitude">payment processor</a> and <a
href="https://github.com/mozilla/monolith">metrics processor</a> and more are
soon to follow.  These projects will be tied together around a central API on
the back end.  We've had partial front end APIs for years (like search) which we
will expand to make the entire site accessible via API.  At that point our front
end code will be completely separated and can be optimized to speak directly to
<abbr title="JavaScript Object Notation">JSON</abbr> APIs instead of pulling
HTML with every request (something which the developers have been demoing the
past couple weeks at our show and tells).  A rough diagram is below, subject to
change, of course.

<img src="/blog/public/img/2013-mkt-services.png" alt="Marketplace Architecture Diagram" />

Some benefits of this approach include:


* Physical separation of code which will easily allow us separate <abbr
  title="Service Level Agreement">SLAs</abbr> or even separate conformance
  agreements, like <abbr title="Payment Card Industry">PCI</abbr> compliance
* Speaking to APIs means we'll have specific failure cases we can write code for
  so when a piece of the site dies the entire site doesn't crash
* Each project can be written to scale horizontally without affecting the other
  projects
* Developers and contributors can focus on a single project without having to
  check out the entire site (and deal with substantial configuration
  maintenance)
* Localizations will be broken up into separate .po files, a long requested
  feature from our localizing friends
* Deployments can happen for specific projects without updating all of them.
  These will be faster, easier to scope, and easier to roll back if necessary
* 3rd parties can build full featured sites off our APIs

There are a couple of downsides:  maintenance/configuration of each project and
integration testing.  The former is diminished a bit because not every developer
works on every project so with some prudent mocking and a few virtual machines
there should be an easy flow there.  The second is something we currently
neglect but will become critical with these changes so expect some solid
developments there.  With all the other work on our schedule I think we'll be
touching parts of this project in every quarter this year.  If you hear the
codename <em>INCEPTION</em> it's referring to this project.
