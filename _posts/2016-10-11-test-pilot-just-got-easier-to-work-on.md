---
layout: post
title: testpilot.firefox.com just got a lot easier to work on
tags:
- Mozilla
---

We originally built Test Pilot on top of Django and some JS libraries to fulfill
our product requirements as well as keep us flexible enough to evolve quickly
since we were a brand new site.

As the site has grown, we've dropped a few requirements, and realized that we
were using [APIs from our engagement team][1] to collect newsletter sign ups,
[APIs from our measurement team][2] for our metrics, and everything else on the
site was essentially HTML and JS.  We used the Django scaffolding for updating
the experiments, but there was no reason we needed to.

*I'm happy to highlight that as of today [testpilot.firefox.com][3] is served
100% statically.*  Moving to flat files means:

* Easier to deploy.  All we do is copy files to an S3 bucket.  No more SQL
  migrations or strange half-pushed states.

* More secure.  With just flat files we have way less surface area to attack.

* Easier to participate in.  You'll no longer need to set up Docker or a
  database.  Just check out the files, run `npm install` and you're done.
  (disclaimer: we just pushed this today, so we actually still need to update
  [the documentation][4])

* Excellent change control.  Instead of using an admin panel on the site, we now
  use GitHub to manage our [static content][5].  This means all changes are
  tracked for free, we already have a process in place for reviewing pull
  requests, and it's easy to roll back or manipulate the data because it's all
  in the repository already.

If you want to get involved with Test Pilot, come join us in [#testpilot][6] (or
[webchat][7])!

[1]: http://basket.readthedocs.io/
[2]: https://wiki.mozilla.org/Telemetry
[3]: https://testpilot.firefox.com
[4]: https://github.com/mozilla/testpilot/blob/master/README.md
[5]: https://github.com/mozilla/testpilot/tree/master/content-src/experiments
[6]: irc://irc.mozilla.org/testpilot
[7]: http://chat.mibbit.com/?server=irc.mozilla.org&amp;channel=#testpilot
