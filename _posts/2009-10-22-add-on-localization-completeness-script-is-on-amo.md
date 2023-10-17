---
layout: post
title: Add-on Localization Completeness Script is on AMO
tags:
- Mozilla
---
<p>The add-on verification suite launched a few months ago and has been refined with each subsequent milestone.  We've changed what it searches for based on feedback and our own findings and earlier this month we made it <a href="https://addons.mozilla.org/en-US/developers/addon/validate">available to anyone on AMO</a>, not just a hosted add-on's authors.</p>
<p>The framework was written in an extensible way so in addition to tweaking the built-in searches, we could also leverage external scripts.  The first such script that is making it to the live site is <a href="http://koala.mozdev.org/drupal/blog/7216">Adrian Kalla's</a> <a href="http://hg.mozilla.org/users/akalla_aviary.pl/silme-patched">localization completeness</a> check.  This script attempts to parse and record all the English string files as a baseline.  Then it looks at each locale and reports any missing files, missing translations, or untranslated strings (translations that exist in the locale but are the same as English).</p>
<p>If you validate an extension now and only have partial L10n coverage, scroll down to the new <abbr title="Localization">L10n</abbr> section and you should see something like this:<br />
<img src="{{ site.baseurl}}/assets/img/l10n_validation.png" alt="Screen shot of the validation tool" /></p>
<p>Thanks to RJ and Adrian for doing all the work on this.</p>
