---
layout: post
title: Committing to SVN securely from a web application
tags:
- Mozilla
---
<p><a href="http://wiki.mozilla.org/Verbatim">Verbatim</a> is the second project
I've been the lead on recently where the requirements included people committing
to <abbr title="Subversion">SVN</abbr> as themselves via the application.  At
first glance this means storing the authentication tokens of the user in plain
text since we'll need to pass them along to SVN whenever they commit.  I wasn't
happy with that solution so after a bit of thinking we came up with an idea that
leaves everything encrypted and doesn't cache any credentials.  It involved
minimal code in Verbatim and minor work on the SVN server.</p>

<p>On the SVN server the first thing we did was to create a special Verbatim
user that can commit to SVN via SSH using a generated key.  We copied this key
to the Verbatim host which allowed us to commit as the verbatim user without
typing a username or password.</p>

<p>The only thing that was added to the Verbatim code was <a
href="http://sourceforge.net/mailarchive/forum.php?thread_name=ADA2D058-904B-44F0-8301-21334A7B6E02%40mozilla.com&forum_name=translate-pootle">a
patch that Dan Schafer cooked up</a> that sets an SVN revision property,
<em>translate:author</em>, to the name of the current user.  When the user
clicks "commit" this property is set and sent along with the commit.</p>

<p>At this point we could commit from the application but it still goes to the
application as the Verbatim user.  We used <a
href="http://svnbook.red-bean.com/en/1.4/svn-book.html#svn.ref.reposhooks">SVN's
hooks</a> to take the next step.</p>

<p>The first script we changed was the pre-revprop-change hook.  This controls
what special revision properties a user can modify when they commit.  <a
href="https://bugzilla.mozilla.org/attachment.cgi?id=337775">Our script</a> adds
the ability to modify svn:author and translate:author.  Before allowing the
modifications the script checks if the user committing is the special verbatim
user to prevent anyone from committing as someone else.</p>

<p>Next we added a <a
href="https://bugzilla.mozilla.org/attachment.cgi?id=339184">post-commit
script</a> that looks for the translate:author property.  If it's found it will
take that value, replace svn:author, and remove translate:author; effectively
making whatever was in translate:author the real author.  This is a
non-versioned change which means there is no commit that needs to happen - the
new author is set immediately.</p>

<p>With these scripts in place we can commit as anyone from the application and
everyone's credentials stay encrypted and secure.</p>
