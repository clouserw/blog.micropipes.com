---
layout: post
title: Splitting AMO and the Marketplace
tags:
- Mozilla
---
Years ago someone asked me what the fastest way to stand up an App
Marketplace was. After considering that we already had several Add-on Types in
AMO I replied that it would be to create another Add-on Type for apps, use the
AMO infrastructure as a foundation for logins/reviews/etc. and do whatever minor
visual tweaks were needed. This was a pretty quick solution but the plan evolved
and "minor visual tweaks" turned into "major visual changes" and soon a
completely different interface. Fast forward a few years and we have two
separate sites (addons.mozilla.org and marketplace.firefox.com) running out of
the same code repository but with different code. Much of the code is crudely
separated (apps/ vs mkt/), but there are also many shared files, libraries, and
utilities, both front and backend. The two sites run on the same servers but
employ separate settings files.

There has been talk about combining the two sites so that the Firefox
Marketplace was the one stop shop for all our apps/add-ons/themes/etc. but there
was reluctance to move down that path due to the different user expectations and
interfaces - for example, getting an app for your phone is a lot different flow
than putting a theme on Firefox. While the debate has simmered with no great
options the consequences of inaction continue to grow.  Today's world:

* Automated unit tests which take far longer than necessary to run because they
  run for both sites.
* Frustration for developers who change code in one area and affect a completely
  different site.
* Confusion for any new employees or contributors as they struggle to set up the
  site (despite our decent documentation).
* A one-size-fits-all infrastructure approach with no ability to optimize for
  the very different sites (API/service based vs standard MVC).

The best way to relieve the stress points above is complete separation of
addons.mozilla.org and marketplace.firefox.com.  [Read the full (evolving)
proposal][0].  Feedback welcomed.

[0]: http://micropipes.com/moz/guillotine/
