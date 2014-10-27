---
layout: post
title: 'AMO Scalability: Then and Now'
tags:
- Mozilla
---
<p>Struggling with scalability on <abbr title="addons.mozilla.org">AMO</abbr> is
nothing new but the tools we use to solve the problems have changed over time.
Here is a bit of information on the performance evolution AMO has gone through.
I wanted to link to the <a href="http://www.archive.org/web/web.php">wayback
machine</a> for all our old versions, but I get "Redirect Errors" for the
addons.mozilla.org domain.  I'll have to make due with code repositories.</p>

<p><a href="http://mxr.mozilla.org/mozilla/source/webtools/update/">Version
1</a> of AMO wasn't concerned with caching.  It was straight <abbr title="PHP:
Hypertext Preprocessor">PHP</abbr> talking directly to a single MySQL box.
Short, easy, and not very scalable.</a></p>

<p><a href="http://lxr.mozilla.org/mozilla/source/webtools/addons/">Version
2</a> of AMO progressed through several caching systems.  The site used the <a
href="http://www.smarty.net/">Smarty template engine</a> so our first step was
to turn on the built in Smarty cache.  That didn't give us the performance we
needed, so <a href="http://morgamic.com/">Mike Morgan</a> started caching page
output in <a href="http://pear.php.net/package/Cache_Lite"><abbr title="PHP
Extension and Application Repository">PEAR</abbr>'s Cache_Lite</a>.  I don't
remember the specifics of this implementation since it was so short lived (less
than a month), but the <a
href="http://bonsai.mozilla.org/cvslog.cgi?file=mozilla/webtools/addons/public/inc/finish.php&rev=HEAD&mark=1.7">CVS
log</a>, mentions problems with "scalability in a clustered environment."  Our
next step was to store the same page output in <a
href="http://www.danga.com/memcached/">memcached</a> instead of Cache_Lite which
brought pretty satisfying results.  Thus began our abuse of memcached.</p>

<p>In addition to memcached and expanding the number of web servers it ran on,
version 2 also boasted two other significant performance improvements. The first
was the ability to talk to a slave database for read-only queries which, when
combined with a load balancer, let us scale database servers horizontally.  The
second was installing a <a
href="http://www.citrix.com/english/ps2/products/product.asp?contentID=21679">NetScaler</a>
in front of addons.mozilla.org giving us the benefits of a reverse proxy cache
and <abbr title="Secure Socket Layer">SSL</abbr> offloading.  These changes
bought us precious time when hoards of Firefox 1.5 users were clamoring for
add-ons.  In fact, I'd say we were in pretty good shape at that point.</p>

<p>Fast forward to <a href="http://svn.mozilla.org/addons/trunk/">Version 3</a>
(the current version).  We've expanded the memcache servers from one to two and
instead of page output we're storing database queries and their results.  We're
still using a single master database but are using two slaves now for read only
queries.  There are several NetScalers around the world caching pages locally[1]
for closer regions.  We've survived quite a while on this system but we're
  starting to push the envelope again and we're going to need to make some
  changes to be able to scale for Firefox 3 and still provide a good user
  experience.  I'll write more about our plans as they develop.</p>

<p>[1] Users who are logged in to AMO don't get the local caches - their
connection is always to San Jose, CA.</p>
