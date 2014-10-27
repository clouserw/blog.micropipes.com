---
layout: post
title: ThreadBubble going the way of the dodo
---
<p>I got the chance to try out the latest version of <a href="http://www.mozillamessaging.com/en-US/thunderbird/3.0a3/">Shredder</a> last night which recently celebrated it's Alpha 3 release <a href="http://www.rumblingedge.com/2008/10/07/shredder-alpha-3-released/">fixing an impressive number of bugs</a>.  Among the heap of bugs is our very own <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=262319">bug 262319</a>; "sort by thread fails to resort on new message."  Two weeks shy of celebrating it's fourth birthday it was squashed and a fix was checked in.</p>
<p><a href="https://bugzilla.mozilla.org/showdependencygraph.cgi?id=236849">A few straggling bugs aside</a>[1] proper message sorting has been achieved and the <a href="http://micropipes.com/code/threadbubble/">ThreadBubble extension</a> is no longer needed.</p>
<p>The latest version, ThreadBubble 0.8, is compatible with Thunderbird versions up to 3.0a2pre and I expect it will be the last version released.  Maybe I'll work on a Firefox extension next...</p>
<p>Anyway, thanks to everyone who tested, used, and gave feedback about ThreadBubble. :)</p>
<p>[1] This is kind of a joke - the <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=236849">parent bug</a> is actually a meta bug for all threaded view issues and I don't know how many of those are confirmed or are relevant to what ThreadBubble fixed.  I do know I filed <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=461100">bug 461100</a> last night which is a new problem with the threaded view as far as I can tell.</p>
