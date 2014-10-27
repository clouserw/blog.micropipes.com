---
layout: post
title: Continuous Integration comes to AMO
tags:
- Mozilla
---
<p>It's time to hail another milestone for <a href="https://addons.mozilla.org/">AMO</a> in our <a href="/blog/2009/11/17/amo-development-changes-in-2010/">epic push for improvements in 2010</a>.  This time I'm happy to announce our <a href="https://hudson.mozilla.org/job/preview.addons.mozilla.org/">Hudson continuous integration server</a> which has been humming along for a few months.</p>
<p><a href="/blog/public/img/hudson_screenshot.png"><img src="/blog/public/img/hudson_screenshot_small.png" title="Hudson Summary Screenshot" /></a></p>
<caption>Hudson Integration Screenshot.  Click to enlarge.</caption>
<p>AMO is the first Mozilla Webdev site to use continuous integration, and it's been a long time coming.  With the way it's currently configured we've got <a href="https://hudson.mozilla.org/job/preview.addons.mozilla.org/512/cobertura/?">code coverage trending</a>, <a href="https://hudson.mozilla.org/job/preview.addons.mozilla.org/512/testReport/?">unit test trending</a>, <a href="https://hudson.mozilla.org/job/preview.addons.mozilla.org/512/violations/?">code quality trending</a>, as well as detailed reports for all the above for every single check in.</p>
<p>If anything fails or oversteps a threshold our IRC bot complains and we can get it fixed up quickly.  It's a boon to productivity to know that all the code being checked in is being tested automatically, plus it gives everyone a stable state to compare to.</p>
<p>Thanks to everyone that helped get Hudson going, from the <a href="http://blog.hudson-ci.org/">people that write it</a>, to <a href="http://blog.mozilla.com/it/">the IT team that keeps it alive</a>, to <a href="http://blog.mozilla.com/webdev/">the webdev team</a> that helped work out the kinks.</p>
