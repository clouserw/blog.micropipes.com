---
layout: post
title: Add-on Statistics Status (part 2)
tags:
- Mozilla
---
<p><em>This is the second update about add-ons' statistics.  <a href="/blog/2009/01/22/add-on-statistics-status/">Read part one</a>.</em></p>
<p>Statistics for both update pings and download counts have been updated beginning with February 1 through today, February 6th.  Some notes:</p>
<ul>
<li>New statistics are stored in <abbr title="Coordinated Universal Time">UTC</abbr> and data processing happens shortly after the logs close.  This means you can expect new data at around 8pm PST or shortly after.</li>
<li><b>Download numbers will drop dramatically</b>.  They have been recorded incorrectly[1] for the past several weeks.  <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=472538" title="Daily &amp; Total Download Counts appear to have been too high since Nov 16">Bug 472538</a> has more details.</li>
<li>We'll begin replacing statistics back to 2008-11-15 over the next few weeks as processing time allows.</li>
<li>An aside that you may not know:  When Firefox looks for an update to an add-on we count that as an "update ping."  If it finds the update it will hit <a href="http://releases.mozilla.org/">releases.mozilla.org</a> directly for the new add-on.  That means that in your current stats numbers updates are not counted as downloads, or another way, "download counts" are the counts of someone actually clicking the "Install Now" button on <a href="https://addons.mozilla.org">addons.mozilla.org</a>.</li>
</ul>
<p>Since we're pulling these statistics from a team dedicated to crunching numbers we're getting richer and more reliable data now.  This frees up our time to fix existing stats bugs and also to add additional data views (like what locale your users are using).  Good things are coming; keep an eye on your stats!</p>
<p><b>Update 2008-02-07</b>:  HP issued a <a href="http://alerts.hp.com/r?2.1.3KT.2ZR.yor8o.Cwf2AM..N.G98I.1lY2.DcJOEZc0">critical alert</a> regarding potential data loss which affected our servers.  Our IT team applied the fix but upon restart discovered it's been way too long since the file system had fsck run on it.  Since there is so much data on the system it will take several more hours to finish, then IT will restore log files, and then we can begin to process the stats for this weekend.  In short, stats won't be current for another day or two.</p>
<p>[1] The technical reason is that Firefox does 2 or 3 GET requests to a server when it installs an add-on.  The filter we had to remove duplicate requests was broken.</p>
