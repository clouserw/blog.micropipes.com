---
layout: post
title: Adding context to AMO .po files
tags:
- Mozilla
---
Adding context to the .po files on <a href="http://addons.mozilla.org/"><abbr
title="addons.mozilla.org">AMO</abbr></a> has been one of our challenges since
we started localizing the site.  The solution we decided to use, <a
href="http://wiki.mozilla.org/Update:Remora_Localization#L10n_standards">place
holder strings</a>, is non-standard and can be difficult to use for someone that
is used to how gettext normally works.

The <a href="http://wiki.mozilla.org/Verbatim">localization tool we've decided
to use for Mozilla projects</a> currently works solely on standard .po files.
Dan Schafer wrote a conversion script that will allow us to convert from the AMO
.po style to the standard gettext style.  In order to create a standard .po file
that can be easily localized we've decided to use a keyword we haven't used
before:  msgctxt.

msgctxt allows us to store the context of a phrase without affecting the actual
phrase.  The script Dan wrote combines two AMO .po files, the English version
and the target locale file, into one.  For example, take these two files:

The English AMO .po file:
> msgid "home_header_greeting"
> msgstr "Hello!"

The French AMO .po file:
> msgid "home_header_greeting"
> msgstr "Bonjour!"

And combine them into a single .po file containing the following:
> msgctxt "home_header_greeting"
> msgid "Hello!"
> msgstr "Bonjour!"

We haven't used the msgctxt keyword until now because it's as of yet
unsupported in PHP but editing tools that support gettext 1.5 and above should
be able to edit the files with no trouble.  We'll still be using the AMO style
.po files in SVN and in the AMO product itself so if you're used to the AMO
style and you plan on continuing to commit directly to SVN it shouldn't affect
your work flow.

If you'd like to use the combined .po style outside of Verbatim there will be
a way to import and export the file format.  If you do edit the file with an
external editor please be careful not to change the context of a string or your
changes won't be saved.

As always, we're happy to hear questions or concerns.  Look us up in <a
href="irc://irc.mozilla.org/#verbatim">#verbatim</a> or leave a comment here if
you want to get in touch with us.
