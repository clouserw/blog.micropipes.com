---
layout: post
title: Using substitution strings in .po files
tags:
- Mozilla
---
A couple years ago [I recommended using fake msgid's in .po files][1] and was,
predictably, met with some argument.   I suggested using this hack because there
wasn't a standard way to store context in a .po file yet.[1]

Since that time <em>msgctxt</em> has become a standard part of gettext and
makes my substitution string recommendation obsolete.  I wanted to officially
come out and say: substitution strings are a pain.  The scripts we used made it
manageable but finding strings in the code meant searching through the .po and
not only was this painful for our developers but I think it confused
contributors as well.

In our latest release, we've converted [AMO][2] to use regular .po files now.
On the off chance someone followed my advice and would like to convert their
site to regular .po files as well,  Zbigniew Braniecki [wrote a bit about the
process][3] and you can grab his scripts (and read about the troubles I had) at
[bug 501988][4].

Since I tagged this post <em>hindsight</em> I guess I should look back and
conclude something too.  Would I do it again?  At the time, there were no great
alternatives.  So, yeah, I would get more opinions on whether the Gnome/KDE
method was better, but I would do it again.  I think it was the best choice out
of several poor ones, but that doesn't mean I'm not very happy to be rid of
them.

[1] To be fair, there <em>was</em> a more common way, used by some KDE and Gnome
projects, which was to put a delimiter in the msgid and keep the context on one
side and the original string on the other.  This is also pretty hacky and you
can [read about Gnome's migration away from that method][5] if you're curious.

[1]: /blog/2007/07/26/ten-tips-for-website-localization/
[2]: https://addons.mozilla.org/
[3]: http://diary.braniecki.net/2009/08/19/amo-loses-accent/
[4]: https://bugzilla.mozilla.org/show_bug.cgi?id=501988
[5]: http://live.gnome.org/GnomeGoals/MsgctxtMigration
