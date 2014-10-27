---
layout: post
title: The Tagging Plan for AMO
tags:
- Mozilla
---
<p>Firstly, thanks for <a href="/blog/2009/03/02/some-considerations-when-adding-tags-to-amo/">all the great feedback</a>.  Something as seemingly simple as tagging gets complex quickly when thought out and the varied perspectives of the community are always great to have.</p>
<p>Allowing full Unicode would let anyone use meaningful tags in their own character sets but would prevent us from offering similar matches and common misspellings.  On the other hand, we support several languages on <a href="https://addons.mozilla.org"><abbr title="addons.mozilla.org">AMO</abbr></a> that don't use the Latin alphabet.  It stands to reason that users would search for tags in their own character sets and would get no results.  There are pros and cons for each choice but we're essentially debating the value of normalization in tagging.</p>
<p>After distilling all the feedback and talking amongst ourselves our overall feeling was that forcing people to convert their input into the Latin alphabet wasn't in the users' best interest.  The <a href="http://www.mozilla.org/about/manifesto">Mozilla Manifesto</a> talks about a global internet that fosters creativity and free expression.  Not supporting a user's native language when we have the option to doesn't feel like the right path to take.</p>
<p>With that in mind our current plan is as follows:</p>
<ul>
<li>Allow full Unicode in tags to the extent we do everywhere else on AMO.</li>
<li>Do no automatic character normalization.  The option of manual normalization (essentially, marking some tags as equivalent) is left open as a future enhancement.</li>
<li>Do automatic white space and capitalization normalization.  Spaces are displayed on an add-on's page but when searching or entering into a <abbr title="Uniform Resource Locator">URL</abbr> spaces are unnecessary.  For example, <em>newyork</em>, <em>new york</em> and <em>New YORk</em> are all equivalent.</li>
<li>A list of suggestions will be provided as the user types.  We may attempt some simplistic character normalization in the suggestions if we can come up with a way that provides enough value to continue to use (perhaps something that is per-language).</li>
<li>White space is trimmed from the beginning and end of tags before they are saved into the database.</li>
<li>Tags are limited to 128 characters and add-ons are limited to 80 tags.</li>
<li>Tags will be comma delimited.  To include a comma in your tag you must use quotation marks.  Quotation marks, whether they are matched or not, are discarded.  Example:  <em>"Portland, OR"</em> will become <em>Portland, OR</em> whereas <em>Portland", OR</em> will become <em>Portland</em> and <em>OR</em>.</li>
</ul>
<p>Additional feedback, as always, is welcome.</p>
