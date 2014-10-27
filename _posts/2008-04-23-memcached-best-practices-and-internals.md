---
layout: post
title: Memcached best practices and internals
tags:
- Mozilla
---
<p>Yesterday, igvita.com published <a
href="http://www.igvita.com/2008/04/22/mysql-conf-memcached-internals/">a short
article summarizing memcached internals and best practices</a>.  It was
originally a talk by Brian Aker and Alan Kasindorf and their slides are
included.  It's a good read and digs into memcached's memory management and
expiration logic.  (Thanks for the heads up, chenb).</p>

<p>I noticed their first best practice for memcached, "Don't think row-level
(database) caching, think complex objects, " is in opposition with what we're
doing on <a href="http://addons.mozilla.org/"><abbr
title="addons.mozilla.org">AMO</abbr></a>.  After stuff like <a
href="https://bugzilla.mozilla.org/show_bug.cgi?id=425315" title="Implement
full-time cache with instant invalidation">bug 425315</a> I completely agree
with them.</p>
