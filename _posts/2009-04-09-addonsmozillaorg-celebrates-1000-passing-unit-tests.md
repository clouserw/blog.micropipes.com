---
layout: post
title: addons.mozilla.org Celebrates 1000 (passing) Unit Tests
tags:
- Mozilla
---
<p>We started writing unit tests for <a href="https://addons.mozilla.org/"><abbr title="addons.mozilla.org">AMO</abbr></a> a few years ago with the best of intentions.  As the tests grew we started running into memory/timeout problems that prevented us from running the tests.  Other priorities took over and since we couldn't run the tests we quit writing them.  The tests got put on the back burner, became stale, and we're for the most part forgotten (an all too familiar story for most developers).</p>
<p>Over the past few months we've been turning that around.  While it's certainly a team effort, it's not stretching the truth to say that <a href="http://blog.jeffbalogh.org/">Jeff Balogh</a> has been the driving force behind making sure our framework can scale and getting our old tests running again.  Thanks to his tireless efforts our latest numbers show over <strong>1200 unit tests</strong>, 1065 of which are passing.</p>
<p>In an effort to prevent them from being forgotten again he also <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=479905">created an IRC bot named bosley</a> who tracks the tests and reminds people when they fail.  Expect to see bosley in <a href="irc://irc.mozilla.org/#amo">#amo</a> soon.</p>
<p>The number of tests and the continuous monitoring of them is a huge milestone for AMO and Mozilla WebDev.</p>
