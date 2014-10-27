---
layout: post
title: CakePHP makes upgrading easy
tags:
- Mozilla
---
<p><a href="http://www.laurathomson.com/">Laura</a> attended <a
href="http://cakefest.org/">CakeFest</a> a couple months ago and got to meet
some core Cake developers in person.  In doing so she let slip that <abbr
title="addons.mozilla.org">AMO</abbr> was running on a pretty old version
(1.1.12 - Released in December of 2006).  Apparently 1.1.15 had some major
performance boosts and since we melted the cluster a few times recently (the <a
href="http://wiki.mozilla.org/Update:Remora_API_Docs">new <abbr
title="Application Programming Interface">API</abbr></a> was the culprit) we
thought it would be a good idea to investigate upgrading.</p>

<p>I downloaded 1.1.15 and 1.1.19, set up a couple symlinks to swap them into my
dev copy and looked at how hard it would be to upgrade.</p>

<p>Hats off to the CakePHP developers.  After merging in a short patch to the
core CakePHP session code, most of the site worked right out of the box.  I made
a few minor tweaks to our code for things that had changed (and filed <a
href="https://trac.cakephp.org/ticket/4140">ticket 4140</a> for them) but all in
all it was pretty painless.  Nice work guys.  It shows a lot of planning and
foresight to make a framework that doesn't have a bunch of code-breaking changes
after years of development.</p>
