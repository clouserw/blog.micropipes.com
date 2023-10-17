---
layout: post
title: Ten years of addons.mozilla.org
tags:
- Mozilla
---
Ten years ago, <a href="http://benjamin.smedbergs.us/blog/">Ben Smedberg</a>
and <a href="http://psychoticwolf.net/">Wolf</a> landed the <a
href="http://mxr.mozilla.org/mozilla/source/webtools/update/">first version of
the code</a> that would make up <abbr title="addons.mozilla.org">AMO</abbr>.
At the end of 2004 it was still called <em>update.mozilla.org</em>, written in
PHP, and was just over 200k, compressed.

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2004.png" />
Behold the home page of update.mozilla.org.

This moved through, I think, 1 major revision "update-beta" which added a
database tabled called <em>main</em> that held all the add-on info.  This came
with some additional fancy styles:

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2005.png" />
I started around 16 months after this foundation was laid.  AMO was essentially
flat HTML files sprinkled with PHP code and database queries, just like
everyone says not to do now.  I think the code was running on a single server
named <em>Chameleon</em> at the time and as we released versions of Firefox it
would get overwhelmed and become unresponsive.  Most of the work at this time
was adding in layers of caching like Smarty and keeping everything in
memcached.  We had a major rewrite in planning (one with more dynamic
possibilities) and I chose <a href="http://cakephp.org/">CakePHP</a> as the
foundation.  That release happened and brought another redesign with it:

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2006.png" />
Check out how those gorgeous pale yellow and faded blue bars complement each
other.  Also note that we're still claiming to be in beta at this point.

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2006.detail.png" />
The Adblock detail page in 2006.  Rated 5 out of 5 by someone named Nick!
Finally, at the end of 2006 the infamous chopper design appeared and took over
the top third of our site:

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2007.png" />
<em>Customizability</em> was the message we were trying to communicate with
this design.  There were some concerns voiced at the time...

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2007.2.png" />
This version followed the first quickly.  The header was reduced slightly, the
content got some more margin, and we started using whitespace to keep things
looking simple.  On the other hand, you'll notice our buttons getting more
complicated - this was the beginning of our button horrors as we started to
customize them for each visitor's device.

Both chopper designs were relatively short lived and, I want to say around
early 2008 we moved to another infamous design - the green candy bar.

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2008.png" />
Here we are emphasizing search.  And how.  There was a rumor we actually stole
this design from another site at the time - I assure you that wasn't the case.

I don't remember the actual date on this one, but let's say 2009 since we seem
to redesign this every year.  This was a complete departure from our previous
work and the design was done from scratch.

<img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2009.png" />
Not a bad looking design and one that served us well.

Finally, our current design:

<p><img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2011.png" /></p>
I still think this is a good looking site.

<p><img style="border:1px solid #aaa;" src="{{ site.baseurl}}/assets/img/amo.2011.2.png" /></p>

This design was also the first year we had a separate mobile site.

I've had the draft for this post written for years and I think it's time just
to hit publish on it - feel free to comment about all the things I forgot.
There should probably also be some disclaimer about me writing this on a Friday
afternoon and I take no responsibility for misinformation or wrong dates. :)

Thanks to <a href="http://blog.fligtar.com/">fligtar</a> for having screenshots
of all the old versions!
