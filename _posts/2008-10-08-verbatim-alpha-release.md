---
layout: post
title: Verbatim Alpha Release
tags:
- Mozilla
- software
---
<p>Last week I connected Verbatim to the addons.mozilla.org <abbr title="Subversion">SVN</abbr> repository and with great help from #verbatim on <abbr title="Internet Relay Chat">IRC</abbr> the blocker bugs have been ironed out.  Special thanks to Rubén Martín (Nukeador) for making the <a href="http://viewvc.svn.mozilla.org/vc/addons/trunk/site/app/locale/es_ES/LC_MESSAGES/messages.po?r1=18049&r2=18488">maiden commit</a>.</p>
<p>The server is a bit more unstable than I'd like[1] but it's usable.  If you'd like to give it a shot to localize the latest <abbr title="addons.mozilla.org">AMO</abbr> changes follow these steps:</p>
<ol>
<li><a href="http://sm-cms01.mozilla.com:8081/en/login.html">Log in with your <abbr title="Lightweight Directory Access Protocol">LDAP</a> account (no need to register separately)</li>
<li>Click "change options" and choose "addons.mozilla.org" and your language</li>
<li>Join #verbatim on IRC and let me know you registered and I'll make you an admin for the locale.  After that other options will appear in the interface.</li>
</ol>
<p>One side note:</p>
<p>To update the .po file from SVN or commit your changes to SVN you need to click "Show Editing Functions" when viewing the LC_MESSAGES folder.  </p>
<p>I'm coming up with a plan to make both the registration process simpler and the updating/commiting more intuitive but for now that's what we've got.  If you'd prefer to keep updating the way you're used to feel free; this is an alpha version and I'm primarily seeking feedback (and hopefully offering some convenience).</p>
<p>If you're interested in learning more about Verbatim there is <a href="https://wiki.mozilla.org/Verbatim">information on the wiki</a> including the current time line in the <a href="https://wiki.mozilla.org/Verbatim:Meeting_Notepad">meeting notepad section</a>.</p>
<p>[1] Due to the way jToolkit works I have to restart the server every time I push a code update which breaks everyone's sessions.</p>
