---
layout: post
title: The most worthless bot on IRC
---
<p>I'm not one to jump on bandwagons just because they're rolling by (even with
<a href="http://xkcd.com/353/">great companions</a>), but I <a
href="http://svn.mozilla.org/projects/kubla/trunk/scripts/kublad.py">started
using Python</a> in one of my projects and I've got to say that I'm pretty happy
with it.  I think <a href="http://docs.python.org/">their documentation</a>
leaves something to be desired but overall the language is pretty intuitive and
it has enough of a following that libraries are plentiful.</p>

<p>One evening I decided I wanted to try making an <abbr title="Internet Relay
Chat">IRC</abbr> bot (because you know we need more of those!).  I'd only worked
with Python briefly before, but armed with the confidence only a language that
you don't know the shortcomings of can bring, I started writing code.  After
less than an hour and about 85 well-spaced lines of code later, <a
href="http://svn.micropipes.com/aaplsauce/trunk/aaplsauce.py">Aaplsauce</a> was
born.  All it does is sit idle in a channel and watch for someone to say
something about <a
href="http://finance.google.com/finance?client=ob&q=AAPL"><abbr title="Apple
Inc.">AAPL</abbr></a>.  After someone mentions the magic phrase the bot looks up
the price and prints it in the channel.  How convenient!</p>

<p>So, nearly worthless?  Absolutely.  But the code is short and easy to write
and python made that possible.  <abbr title="&quot;Thanks.&quot;  That's right.
I abbr'd it.">Thx</abbr> Python.</p>
