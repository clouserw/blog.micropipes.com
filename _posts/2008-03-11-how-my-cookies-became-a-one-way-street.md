---
layout: post
title: How my cookies became a one way street
tags:
- Mozilla
---
I've been playing with CakePHP's session code lately and ran across an
interesting (read: nerdy) problem with cookies on <a
href="http://addons.mozilla.org/">AMO</a>.

First, some background:

The uniqueness of a cookie in the browser is determined by all the attributes
when it's set (not just it's name).  That means I can have multiple cookies
named <q>AMOv3</q> as long as another attribute (eg. path) is different when I
set the second cookie.

According to <a href="http://www.faqs.org/rfcs/rfc2109.html">RFC 2109</a>:

> If multiple cookies satisfy the criteria [...] they are ordered
> in the Cookie header such that those with more specific Path attributes precede
> those with less specific.

In PHP, however, cookies are indexed in the $\_COOKIE variable by name, which
means I can send several cookies with the same name and only the first cookie
will show up. <sup>[1]</sup>


So, what's this have to do with AMO?  For some reason, CakePHP hasn't been
consistent in the past regarding cookie paths. Sometimes they were <q>/</q>
(which is correct), sometimes they were something else like
<q>/en-US/firefox/users/</q> and sometimes users had multiple cookies with
different paths.

From the <a href="http://php.oregonstate.edu/setcookie">PHP manual</a>:

> Cookies must be deleted with the same parameters as they were set with. If the
> value argument is an empty string, or FALSE, and all other arguments match a
> previous call to setcookie, then the cookie with the specified name will be
> deleted from the remote client.

When a browser sends a cookie back to a server it only sends the name and value.
If a cookie was set with a path that I don't know I have no way to remove that
cookie!

To compound the problem, if a cookie with the same name has a more specific
path, it shows up in $\_COOKIE and there is no indication the other cookie even
exists.  This means on the front page your session can be fine and after
clicking on a deeper URL you're suddenly requesting a session that has been
expired long ago.

We rolled out a change to session handling last week that prevented myself and
another developer from logging in because we had a mess of cookies with
different paths.  I haven't had a barrage of emails so I don't think it's
affected many people, but if you have any troubles with logging in please let me
know.  If you're in a hurry, clearing your cookies for the addons.mozilla.org
domain will fix any problems.

For the record, any new login cookies on AMO will expire when the browser closes
which should prevent stale cookies from coming back to haunt us.

[1] If you need to get at all the cookies the browser is sending, you'll have to
dig through $\_SERVER['HTTP\_COOKIE'] manually.
