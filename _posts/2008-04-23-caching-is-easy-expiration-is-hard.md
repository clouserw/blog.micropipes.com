---
layout: post
title: Caching is easy; Expiration is hard
tags:
- Mozilla
---
Still on a high from [our success with memcached][1] in <abbr
title="addons.mozilla.org">AMO</abbr> version 2, we decided to go a fairly
common route and cache query results in version 3.  This performs admirably
particularly with our [ridiculously long and slow queries][2].  Over time,
though, the popularity of the site and the load on the servers climb, and soon
we're looking at slowness issues again.  On a rough day we decided to increase
the expiration timeout for our queries in memcached from a minute to around an
hour.  This gives the database servers some breathing room but causes excessive
delay on the AMO site when add-ons are updated and things like [bug 425315][3]
and it's friends are born.  Weird things happen when parts of a site expire at
different times and consequently user experience (particularly add-on
developers) suffers.

The problem we're running into in the bug linked above is knowing when to
expire a cache.  Consider when an add-on author updates the summary of their
add-on.  We know we'll have to flush the queries on that page out of memcached,
and that's easy enough, but what about all the other places the summary is used?
Search results pages, add-on detail pages, recommended lists, the <abbr
title="Application Programming Interface">API</abbr>, etc.  Now we've got to
figure out the queries used on those pages and expire them too.  Suddenly I'm
wishing we were caching objects in memcached instead of queries.

I looked in to other ways to use memcached and they all have their pros and
cons.  Caching entire pages means we'd have to store different versions for a
person that is logged in vs. logged out and also what permissions they had
(pages have different options for localizers, admins, developers, etc.).
Caching objects is attractive, but the way [CakePHP][4] does queries makes this
a non-option (namely, it's not asking objects for values, it does joins directly
on the db).  Directly caching queries seems like the best fit because we can
affect just the parts of the pages we want and it will work with CakePHP's
current system...just as soon as we figure out how to relate updating a row to
all of it's associated queries.

I attached an idea to the bug but regardless of the process we use, figuring
out how to implement a full time cache that we can expire on the fly is going to
be an important step in keeping the AMO site usable as our traffic
increases.

[1]: http://micropipes.com/blog/2008/04/18/amo-scalability-then-and-now/
[2]: http://blog.mozilla.com/webdev/2007/04/18/teaching-cakephp-to-be-multilingual-part-3/
[3]: https://bugzilla.mozilla.org/show_bug.cgi?id=425315 "Implement full-time cache with instant invalidation"
[4]: http://cakephp.org
