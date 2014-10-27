---
layout: post
title: Libraries to connect to a Citrix NetScaler or Zeus Traffic Manager
tags:
- Mozilla
---
<p>The first front end cache we used on <a href="https://addons.mozilla.org/">AMO</a> was the <a href="http://www.citrix.com/English/ps2/products/product.asp?contentID=21679">Citrix NetScaler</a>.  I've <a href="http://micropipes.com/blog/2008/07/14/planning-your-api-is-important/">complained about it's API before</a> but apparently never announced the library I wrote to purge items from the cache.  So, a little late, but I have <a href="http://viewvc.svn.mozilla.org/vc/libs/ns-api/">some reusable PHP code that will talk to your NetScaler</a> and let you expire objects.</p>
<p>We hit some limitations with the NetScaler that we weren't happy with.  Cost aside, it ignored some pretty standard stuff like the <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44">HTTP Vary Header</a>.  After working around that for years we switched to the horizontally scalable <a href="http://www.zeus.com/products/traffic-manager/index.html">Zeus Traffic Manager</a> (at that time, referred to as ZXTM).  We've been pleased with our choice and six months ago I wrote a <a href="http://viewvc.svn.mozilla.org/vc/libs/zxtm-api/">similar PHP library that allows you to connect to Zeus's API</a>.  Time and priorities being what they are, we never implemented it in production.</p>
<p>Finally, the real point to this post, last night I wrote a <a href="http://github.com/clouserw/hera">python library that will expire content from Zeus</a>.  We'll roll this into our migration and waiting on content to expire from Zeus should be a thing of the past.</p>
<p>As always, if you can use the libraries, feel free.  They all have READMEs with examples.</p>
