---
layout: post
title: Test Pilot Legacy Program Final Review
date: 2016-10-27 01:55:00 -0800
tags:
- Mozilla
---

One of my Q3 goals was to migrate the Legacy Test Pilot users into our new
Test Pilot program ([some background on the two programs][1]).  The previous
program was similar in that people could give feedback on experiments, but
different enough that we didn't feel comfortable simply moving the users to the
new program without some kind of notification and opting-in.

We decided the best way to do that was simply push out a new version of the
legacy add-on which opened a new tab to the Test Pilot website and then
uninstalled itself.  This lets an audience interested in testing experiments
know about the new program without being overbearing.  Worst case scenario, they
close the tab and have one less add-on loading every time Firefox is started.

In our planning meeting it was suggested that with this method getting three
percent of users from the old program to the new would be a reasonable
compromise between realistic and optimistic.  I guffawed, suggested that the
audience had *already opted-in once*, and put 6% in as our goal.  Spoiler alert:
They were right and I was wrong.

I'll spare you the pain of writing the add-on (most of the trouble was that the
legacy add-on was so old you had to restart Firefox to uninstall it which really
broke up the flow).  On August 24th, we [pushed the update to the old program][2].

<img src="/blog/public/img/2016-testpilot-adu.png" title="Graph of daily usage" />

In the daily usage graph, you can see we successfully uninstalled ourselves from
several hundred thousand profiles, but we still have a long tail that doesn't
seem to be uninstalling.  Fortunately, AMO has really great statistics
dashboards ([these stats are public, by the way][3]) and we can dig a little
deeper.  So, as of today there are around 150k profiles with the old add-on
still installed.  About half of those are reporting running the latest version
(the one that uninstalls itself) and about half are disabled by the user.  I
suspect those halves overlap and account for 75k of the installed profiles.

The second 75k profiles are on older add-on versions and are not upgrading to a
new version.  There could be many reasons when we're dealing with profiles this
old: they could be broken, they might not have write permissions to their
profile, their network traffic could be being blocked, an internet security
suite could be misbehaving, etc.  I don't think there is much more we can do
for these folks right now, unfortunately.

Let's talk about the overall goal though - how many people joined the new
program as a result of the new tab?

<img src="/blog/public/img/2016-testpilot-conversions.png" title="Graph of conversions" />

As of the end of Q3, we had just over 26k conversions making for a *3.6%
conversion rate*.  Quite close to what was suggested in the original meeting by
the people who do this stuff for a living, and quite short of my brash guess.

Overall we got a 0.6 score on the [quarterly OKR][4].

----------

Since I'm writing this post a few weeks after the end of Q3, I can see that
we're continuing to get about 80 new users per day from the add-on prompt.
Overall that makes for about 28.5k total conversions as of Oct 27th.



[1]: http://micropipes.com/blog/2016/01/27/meet-the-new-test-pilot/
[2]: http://micropipes.com/blog/2016/08/24/time-to-upgrade-from-test-pilot-to-test-pilot/
[3]: https://addons.mozilla.org/en-US/firefox/addon/test-pilot/statistics/
[4]: https://wiki.mozilla.org/Test_Pilot/2016Q3
