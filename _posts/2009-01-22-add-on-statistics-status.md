---
layout: post
title: Add-on Statistics Status
tags:
- Mozilla
---
<p>Add-on statistics have been intermittent for a couple months and are just recently getting the attention they need.  </p>
<p>Our current process is to count download statistics once per day and update ping statistics once per week (update pings are a sampling of the complete set).  The reliability of the script generating these statistics has been falling as our data size has grown and we've had several bugs filed regarding the numbers it's produced.  Most of the time they are relatively small fixes and the script continued to limp along.</p>
<p>Currently we're facing questionable results in both sets of statistics (<a href="https://bugzilla.mozilla.org/show_bug.cgi?id=468570">bug 468570</a> for update pings, <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=472538">bug 472538</a> for download counts).  I've been debugging the update pings script and despite solving some problems we're continuing to see the script fail to run properly.</p>
<p>Parallel to AMO development, <a href="http://daniele.livejournal.com/">Daniel Einspanjer</a> has been working on a larger statistics parser that will aggregate data from many Mozilla sites into a dashboard with easy visualizations.  It turns out he's already processing the <abbr title="addons.mozilla.org">AMO</abbr> logs and pulling out more data than us more often and in less time.  </p>
<p>With a system like that available it doesn't make sense for us to continue to develop (and, in this case heavily modify) our local statistics scripts.  With that in mind, our next steps are:</p>
<ol>
<li>Verify the results we (used to) get with the AMO scripts match those of the new system</li>
<li>Create a transformation script to push the data from Daniel's project to the AMO database</li>
<li>Turn off the AMO scripts</li>
<li>Back fill statistics through at least November 15th, 2008 to replace our flailing stats.  If the comparisons in step 1 reveal miscounting from before that we'll back fill as far as we need to.</li>
</ol>
<p>These steps will let us meet the immediate goal of getting the statistics we offer now to be reliable and complete.  In the future we can look at pulling additional data from the new metrics system.  The target date to switch to the new system is the end of next week, Jan 31 2009.  Once we make the switch we can evaluate how long the parsing takes and give an estimate of how long back filling will take.  As always, let me know if there are any concerns.</p>
<p><em><strong>Update 2009-02-02:</strong></em>  We compared the scripts' results and found a discrepancy among add-ons that have significant external download numbers.  The current stats script verified the GUID matches and then counted the update.  The new stats script verified the GUID and the version before counting the update.  This means if a specific version isn't hosted on AMO the new script doesn't count it.  I think the current method of verifying only the GUID is more useful to authors and the new script is being changed.  That means we'll have to re-run and re-compare the numbers (a single day is taking about 5 hours now).  Other numbers are showing early promise.  I'll continue to update as we progress.</p>
