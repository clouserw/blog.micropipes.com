---
layout: post
title: "Some GMail filters to make sorting through Mozilla email easier"
tags:
- Mozilla
---

I use some GMail filters to help sort out the flood of emails I get from Mozilla
projects.  They help me identify bugs and issues I've been asked for
information on versus the mail I get from, for example, being an owner for our
GitHub organization.

I thought I blogged about this before but I couldn't find the post, and maybe
Google's new Inbox will make this irrelevant, but in the mean time:

I have some labels set up in Gmail:

<img src="/blog/public/img/2017-email-list.png" title="Some labels in GMail" />

And some filters:

```
Matches: from:(bugzilla-daemon@mozilla.org) to:(wclouser@mozilla.com) ("X-Bugzilla-Reason: Reporter" OR "X-Bugzilla-Reason: CC")
Do this: Apply label "bug/cc"
```

```
Matches: from:(bugzilla-daemon@mozilla.org) to:(wclouser@mozilla.com) "X-Bugzilla-Severity: blocker"
Do this: Apply label "bug/blocker"
```

```
Matches: from:(bugzilla-daemon@mozilla.org) to:(wclouser@mozilla.com) "X-Bugzilla-Assigned-To: wclouser@mozilla.com"
Do this: Apply label "bug/mine"
```

```
Matches: from:(bugzilla-daemon@mozilla.org) to:(wclouser@mozilla.com) "needinfo?wclouser"
Do this: Apply label "bug/mine"
```

```
Matches: from:(notifications@github.com)
Do this: Skip Inbox, Apply label "github"
```

```
Matches: from:(notifications@github.com) "You are receiving this because you are on a team that was mentioned."
Do this: Skip Inbox, Apply label "github/mine"
```

```
Matches: from:(notifications@github.com) to:(wclouser@mozilla.com) "You are receiving this because you were mentioned."
Do this: Apply label "github/mine"
```

Then I just keep an eye on the labels where things are assigned to me and I can
mostly stay up with requests.  This system isn't perfect -- how do you handle
the mail? :)
