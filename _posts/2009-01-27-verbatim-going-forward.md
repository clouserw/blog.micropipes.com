---
layout: post
title: 'Verbatim: going forward'
tags:
- Mozilla
---
<p>According to the <a href="/blog/2008/11/19/high-level-verbatim-plan/">high level plan</a>, we're currently on step 4.  The Mozilla branch has been merged back into Pootle's trunk and work on the branch has been discontinued.</p>
<p>While writing code it became apparent that the framework Pootle was built on, <a href="http://jtoolkit.sourceforge.net/">jToolkit</a>, had some shortcomings that were making it difficult to work with (not to mention development had been stopped on it since 2006).  The decision was made to migrate the back end of Pootle from jToolkit to <a href="http://www.djangoproject.com/">Django</a>.  This wasn't something I had counted on when I originally made the time line for Mozilla using Pootle but it was a necessary delay.  During the transition, forward progress, at least on the Mozilla side, was halted.  In November and December, the translate.org.za team did some fantastic work and completely replaced jToolkit.</p>
<p>Thanks to a lot of work from everyone and a bunch of unit tests the django based system reached parity with the old system rapidly.  The Pootle team is expecting to release a new version around the end of this month.  At that time I'll upgrade our <a href="https://sm-cms01.mozilla.com:8081/">alpha version</a> and re-enable the features I've had to disable.  I'm expecting the upgrade to solve a lot of the scalability problems we've been having and then we can start advertising our install more and expanding the projects it works with.</p>
<p>Once I do the upgrade Mozilla will be running a stock version of Pootle which I expect to continue from this point forward.  Any patches Mozilla contributes back will be generic enough to be useful to anyone and will land on trunk.</p>
<p>We've created a <a href="http://translate.sourceforge.net/wiki/pootle/planning/2009/goals">2009 idea/goal wiki page</a> which will be distilled into a project road map.  There are some exciting features coming down the pipeline, bringing a lot of improvements (particularly with the user interface) with them.  As an added bonus, the new Django framework will allow us to progress faster with new features and it will be easier for more people to contribute code.</p>
<p>Thanks for your patience.</p>
