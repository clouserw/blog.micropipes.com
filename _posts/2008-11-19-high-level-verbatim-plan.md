---
layout: post
title: High-level Verbatim plan
tags:
- Mozilla
---
<p>Looking over what I've written about Verbatim I realize that I've never talked about the overall plan on here.  Even though we're well into it at this point it doesn't hurt to review.</p>
<p>The original plan for Verbatim was to branch Pootle and continue to merge code between the branch and trunk as features were developed.  As we developed code we realized this just creates more work for developers and makes users have to choose between two branches.  A better method is just to have everyone commit to trunk and write the code in such a way that any site specific code is maintained in configuration files which is what the current plan entails.</p>
<p><strong>Step 1: Branch Pootle.</strong>  <a href="http://www.translate.org.za/blogs/wynand/">Wynand</a> created the <a href="http://translate.svn.sourceforge.net/viewvc/translate/src/branches/mozootle/">Mozootle</a> branch as a place for Mozilla developers to commit.  For the record, Verbatim is the name of the project, Mozootle is the name of the actual branch in the repository; effectively, they are interchangable.</p>
<p><strong>Step 2: Develop Mozootle.</strong>  We used Bugzilla to <a href="http://tinyurl.com/58l55v" title="Verbatim Resolved Bugs (Bugzilla)">track our changes</a> and there are still plenty to do but the first milestone is closed at this point.</p>
<p><strong>Step 3: Merge Mozootle to Trunk.</strong>  This is the stage we're currently at.  The <a href="http://translate.org.za/">translate.org.za team</a> has been reviewing the changes in Mozootle and planning out the merging strategy.  There is a <a href="http://translate.sourceforge.net/wiki/developers/mozootle#mozootle_issues">fast moving wiki page</a> tracking issues with the merge right now.  Our current goal is to resolve these and merge in the next couple days.</p>
<p><strong>Step 4: Continue development on Trunk.</strong>  The plan after the merge is for all developers to continue committing code into the Pootle trunk.  What "development" means is a post in itself so I'll cut this off here.</p>
<p>In hindsight the whole branching and merging process seemed necessary at the time but it doesn't feel like we gained much.  Next time I think we'll just skip the branch.</p>
