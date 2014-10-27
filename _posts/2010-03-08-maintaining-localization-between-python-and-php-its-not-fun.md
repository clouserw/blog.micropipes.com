---
layout: post
title: Maintaining localization between Python and PHP (it's not fun)
tags:
- Mozilla
---
<p>I reached my hand into the barrel of problems <a href="/blog/2009/11/17/amo-development-changes-in-2010/">our migration to Python</a> is going to cause and came up with Localization.  It figures.</p>
<p>First out of the chute was the .po files.  It turns out the actual formatting is different between the two languages.  PHP uses <em>%1$s</em> for its substitutions, but python uses either named variables like <em>(num)s</em> or integers like <em>{0}</em>.  For the record, they both support <em>%s</em> when you don't need to order the substitutions.<br />
PHP example:<br />
<code>I have %2$s apples and %1$s oranges</code><br />
Python example:<br />
<code>I have {1} apples and {0} oranges</code></p>
<p>Since I've worked with the <a href="http://translate.sourceforge.net/wiki/">Translate Toolkit</a> before, I decided to write a script to convert between the two formats.  If you find yourself in the same unfortunate boat as me, behold<br />
<a href="http://translate.svn.sourceforge.net/viewvc/translate/src/trunk/translate/tools/phppo2pypo.py?view=markup">phppo2pypo</a> and <a href="http://translate.svn.sourceforge.net/viewvc/translate/src/trunk/translate/tools/pypo2phppo.py?view=markup">pypo2phppo</a> to convert between the two types.</p>
<p>Crisis averted, right?  Oh, that's just scratching the surface.  Remember <a href="/blog/2008/07/09/adding-context-to-amo-po-files/">how happy I was that PHP finally started supporting msgctxt</a>?  Well, Python has had <a href="http://bugs.python.org/issue2504">a patch for it since 2008</a> but no one has bothered to land it.  I wrote a new <a href="http://github.com/clouserw/tower/blob/master/l10n/__init__.py">ugettext() and ungettext()</a> that recognizes context in the .po files.  To use simply do: <em>from l10n import ugettext as _</em> at the top of your file.</p>
<p>Along with adding msgctxt support, those two functions also collapse consecutive white space.  We're using <a href="http://jinja.pocoo.org/2/">Jinja2</a> with <a href="http://babel.edgewall.org/">Babel</a> and the <a href="http://jinja.pocoo.org/2/documentation/extensions">i18n extension</a> as our template engine.  Jinja2 has a concept of stripping white space from the beginning or end of a string but does nothing about the middle.  A paragraph of text in a Jinja2 template would look like:<br />
<code><br />
  {% raw %}{% trans -%}{% endraw %}Mozilla is providing links to these applications<br />
  as a courtesy, and makes no representations regarding the<br />
  applications or any information related thereto. Any questions,<br />
  complaints or claims regarding the applications must be<br />
  directed to the appropriate software vendor.<br />
  {% raw %}{%- endtrans %}{% endraw %}<br />
</code></p>
<p>That's a decent looking template, right?  Yeah, well, when Babel extracts that, it includes all the line breaks too, giving you something <a href="http://bitbucket.org/plurk/solace/src/tip/solace/i18n/messages.pot#cl-625">like this</a>.  The localizers would revolt if I sent them that, so I added in auto white-space collapsing.  Getting Babel to use the new functions means <a href="http://github.com/clouserw/tower/blob/master/tower/management/commands/extract.py">a new extraction script</a>.</p>
<p>At this point, we're extracting strings from our new code and we can convert between Python and PHP files.  All we need now is a Frankenstein mix of xgettext functions to act as glue.  Meet the <a href="http://github.com/clouserw/tower/blob/master/l10n/management/commands/amalgamate.py">amalgamate script</a> that uses the pypo2php scripts, concatenates the .pot files, and merge updates each locales .po file.  After that it's <a href="http://viewvc.svn.mozilla.org/vc?revision=63671&view=revision">quick tweaks to the build scripts</a> to create z-messages.po files and we're done.</p>
<p>So, all that said, the new process for L10n, while we're in this transitional phase, is:</p>
<ol>
<li>From the PHP code, run <em>locale/extract-po-remora.sh</em>.  That pulls everything from all the PHP files, creates <em>locale/r-keys.pot</em>, updates the messages.po file for each locale, and compiles them.  Life used to be so simple.</li>
<li>From the python code, make sure you're up to date, then run <em>./manage.py extract</em>.  That will pull everything from the python code and templates and create <em>locale/z-keys.pot</em>.</li>
<li>Run <em>./manage.py amalgamate</em>.  That will merge the z-keys.pot into the PHP messages.po files.</li>
<li>Localizers can make their changes as usual, and commit back to messages.po.</li>
<li>From PHP, <em>locale/copy-to-zamboni.py locale</em> will create z-messages.po files in the Python format. We could skip right to .mo files, but in case something goes wrong I want to see the .po files.</li>
<li>Then, like today, <em>locale/compile-mo.sh locale</em> will compile all the .po files.</li>
</ol>
<p>After all those steps are done, we've got duplicate .mo files, aside from formatting, and each application can look at its own .mo to get the strings it needs.  All this code is just a big band-aid and there are plenty of things that are more fun than juggling L10n between two applications across two <abbr title="Revision Control Systems">RCS</abbr>s.  But we knew what we were getting in to.  I'll post something more positive later to help justify it. :)</p>
