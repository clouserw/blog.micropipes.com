---
layout: post
title: Planning your API is important
tags:
- Mozilla
---
<p>I'm upgrading some code I wrote to talk to a new version of the <a
href="http://www.citrix.com/English/ps2/products/product.asp?contentID=21679">Citrix
NetScaler</a>'s <abbr title="Application Programming Interface">API</abbr>.  The
NetScaler's manuals (that's right, plural) weigh in at a combined 1114 pages so
documentation isn't a problem and their implementation is a breeze using <abbr
title="Web Services Definition Language">WSDL</abbr> over <abbr title="Simple
Object Access Protocol">SOAP</abbr>.  However, some of the core changes left me
scratching my head.  Case in point:</p>

<p>To get an object out of the cache in the previous version the method signature was:</p>

`getcacheobject(string $url, string $host, unsignedInt $port)`

<p>$url in this case is what is commonly referred to as the "path" in a standard
<abbr title="Uniform Resource Locator">URL</abbr>; e.g. /en-US/index.html.
That's simple enough to use, let's see what the new version has:</p>

`getcacheobject(string $url, unsignedLong $locator, string $host, unsignedInt $port [...]`

<p>$locator is an internal id for a cache object which is defintitely something
I should be able to use to expire content, but what is it doing in the middle of
my url+host pair?  The error messages are happy to let me know that I
<b>can't</b> pass both $url and $locator to the same call and if I pass $url I
<b>must</b> pass $host.  That means I will always have be passing a null value
in either the first or second parameter.</p>

<p>And if you're thinking it's for consistency with other methods, think again.
To flush an object we've got:</p>

`flushcacheobject(unsignedLong $locator, string $url, string $host, unsignedInt $port [...]`

<p>Moral of the story: planning and consistency makes happy programmers;
particularly with an API.</p>
