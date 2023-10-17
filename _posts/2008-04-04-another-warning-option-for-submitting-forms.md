---
layout: post
title: Another warning option for submitting forms?
tags:
- Mozilla
---
<p>These are our current options for submitting forms in Firefox 3:<br />

<img src="{{ site.baseurl }}/assets/img/firefox_security_options.png" alt="Firefox security
options dialog" /></p>

<p>I don't know anyone that has the "I submit information that's not encrypted"
option checked.  We used to prompt for submitting information that was
unencrypted, next we added an option on the dialog that disabled the warning
(and was checked by default), and finally we removed the warning by default all
together.  People submit so much information via searches, surveys, voting,
sending quick messages, etc. that it would just get in the way and be
ignored.</p>

<p>I've noticed lately that <a href="http://www.wachovia.com/">a</a> <a
href="http://www.scottrade.com/">lot</a> <a href="http://geico.com">of</a> <a
href="http://www.tdameritrade.com">sites</a> are showing login forms on
unencrypted pages but submitting them via <abbr title="Secure Socket
Layer">SSL</abbr> to their target pages.  This is a secure method of logging in
but it's started to train me to not look for a secure connection before I log in
and that's not a good idea in the long run.</p>

<p>I think our current option is too broad, so I'm proposing that we add an
option that says "I submit credentials that aren't encrypted" or a sub-option
for the current text that says something about "unless I'm sending a
  password."</p>

<p>In more technical language:  If a user POSTs a form containing an input of
type="password" to a non-encrypted page we should show a warning.</p>

<p>This would mean regular searches, filling in surveys, anonymous voting and
polls would all pass transparently if unencrypted, but when you got to a form
with a password you would be warned.</p>

<p>I bounced this idea off a channel in <abbr title="Internet Relay
Chat">IRC</abbr> and no one said I was nuts so I figured I'd take it here.  It
seems like too small of a feature to make an add-on out of but I might if I get
some free time.  What do you think?</p>
