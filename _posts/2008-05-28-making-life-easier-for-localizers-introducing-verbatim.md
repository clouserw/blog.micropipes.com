---
layout: post
title: Making Life Easier for Localizers - Introducing Verbatim
tags:
- Mozilla
---
The webdev and <abbr title="Localization">L10n</abbr>-drivers teams have been
talking about implementing an online localization tool for a few months and I'm
happy to report that a plan is progressing.  Seth Bindernagel has been <a
href="http://blog.mozilla.com/seth/category/l10n-tools/">giving updates</a>
about the planning process and the direction we're going in.  Our planning
decisions will probably come up but my focus here will be on the actual
implementation of the tool.

We've decided to use the codename <strong>Verbatim</strong> to refer to this
project.

I've started <a href="http://wiki.mozilla.org/Verbatim">some wiki pages</a>
that are short but growing.  As usual there is a <a
href="http://wiki.mozilla.org/Verbatim:Meeting_Notepad">meeting notepad</a>
which anyone is welcome to peruse.  The wiki page offers a brief description but
I can give a short summary of our current situation and where I'd like to see it
go.  This tool will be used for both the Firefox browser and Mozilla web sites.
I expect my posts to lean towards talking about the web since that's where my
brain is but it's important to keep both in mind.

The current situation:

* L10n projects are scattered around in different places.  Most web sites are in
  <abbr title="Subversion">SVN</abbr> but the browser's L10n is in <abbr
  title="Concurrent Versioning System">CVS</abbr>.
* <a href="http://wiki.mozilla.org/Verbatim:Development/filetypes">L10n projects
  use several different formats</a>.
* There are unnecessarily complex permissions in our system.  Localizers need an
  <abbr title="Lightweight Directory Access Protocol">LDAP</abbr> account and
  then have to be specifically granted permission in the SVN directory to
  commit.  Sometimes those two get decoupled and strange permission errors
  happen.
* Some of our projects use a potentially slow process.  For example, on <a
  href="https://addons.mozilla.org/">AMO</a>, some localizers still add updated
  translations to a bug as attachments and then I commit them to SVN manually.
  This takes time and if I don't get to it for a while the localizer is stuck
  waiting on me to update before they can verify the changes.
* When we add or change a string on a web site we generally just email the
  dev-l10n-web mailing list which is easy to miss.  There is an <abbr
  title="Really Simple Syndication">RSS</abbr> feed coming out of SVN but that's
  still not an ideal notification system.

The plan:

* Provide a central point of localization where someone can see all L10n
  projects for a locale and the amount of work to be done on each.
* Provide a common interface for localizing all of our different file types.
* Provide an easy way to change the strings online[1].
* Provide an easy way to be notified of new and changed strings.
* Optionally, provide the public with a way to suggest changes to existing
  strings.  L10n leaders will be able to approve or reject these suggestions at
  their convenience.

After reviewing many tools online, in the interest of time, completeness, and
alignment with the plan, the webdev and L10n-drivers team have decided to use <a
href="http://translate.sourceforge.net/wiki/">Pootle and the Translate
Toolkit</a> for our initial release.  Pootle in it's current form already
implements the basics of Firefox L10n and supports regular .po files.  The
webdev goal over the next few weeks will be to setup an official Pootle
development area and start figuring out how to convert our L10n projects' file
types to something Pootle can import and export.

I'm hoping these changes will encourage new users to get involved and make
things easier for our long time contributers.  The plan is still in development
and, as usual, input is welcome.  Real time discussion is easiest in <a
href="irc://irc.mozilla.org/verbatim">#verbatim</a> on <abbr title="Internet
Relay Chat">IRC</abbr>.  Email and comments here are effective as well.

[1]  Just to be clear, I don't want this tool to become a bottleneck or
hinder localizers that have a good process down.  <strong>It will still be
possible to do check-ins to the repositories manually without using the web
interface</strong>.  The current Pootle web interface can be <a
href="http://pootle.locamotion.org/">played with</a> or you can <a
href="http://l10n.mozilla.org/af/screencasts/mozilla-pootle.ogv">watch a
screencast</a> for more details.
