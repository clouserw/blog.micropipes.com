---
layout: post
title: Verbatim Server Downtime
tags:
- Mozilla
---
<p>Translate Toolkit 1.3.0 <a href="http://sourceforge.net/mailarchive/message.php?msg_name=1233763860.13980.10.camel%40localhost">was released</a> a few days ago.  I was following along with trunk on my development box and I wanted to upgrade our alpha install to take advantage of the new features (namely, speed improvements) and the django framework.</p>
<p>I attempted this tonight and it was not a pretty upgrade (or install, for that matter).  Among the medley of problems is <a href="http://code.djangoproject.com/ticket/6548">Django ticket #6548</a>.  Django assumes it's not behind an SSL proxy so when it does any redirects it doesn't use https.  This means logging in and logging out work on our server but the user is presented with a jarring "bad request" interstitial.</p>
<p>The current status is that user accounts are not migrated and, even if they were, I can't seem to set permissions for projects.  Since there are some odd problems that we haven't seen elsewhere and this is an alpha install I'm going to leave it as is and debug some of the issues over the next few days.  Expect downtime.  If there are questions visit #verbatim on irc.mozilla.org.</p>
