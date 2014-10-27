---
layout: post
title: 'Status Watch: An add-on for noticing HTTP error codes'
tags:
- Mozilla
---
<p>Often on complex pages with many assets it can be easy to overlook assets which don't load.  Usually they are minor JS, CSS, or tracking pixels which aren't noticed until you've spent way too long trying to track down the problem (or a month later you log into your stats dashboard to discover you haven't been collecting stats).</p>
<p>With the launch of the new <a href="https://builder.addons.mozilla.org">Add-on Builder</a> (still an alpha product, but usable) I decided to make my first Jetpack to fix this.</p>
<p>In only about <a href="https://builder.addons.mozilla.org/addon/1000273/latest/">20 lines of code</a> I was able to look for any 4xx or 5xx errors in the HTTP traffic and show a brief notification to the user about what went wrong and where.  The builder was a great development experience (lack of documentation aside) and was a breeze to do something relatively complex.</p>
<p>If you've wanted a similar add-on, feel free to use <a href="https://addons.mozilla.org/en-US/firefox/addon/status-watch/">Status Watch</a>.  It's a Jetpack so you'll need Firefox 4, but on the bright side, you won't even need to restart the browser.  Just click and go.</p>
<p><em>I've had some requests to support a whitelist of sites so you don't get notifications all over the web and I'll add that when I get time.  It's surprising how many sites have 403s and 404s though.</em></p>
<p>Update 2011-02-17:  Version 2 is on AMO now which supports a whitelist.  See the <a href="https://addons.mozilla.org/en-US/firefox/addon/status-watch/">AMO page</a> for details.</p>
