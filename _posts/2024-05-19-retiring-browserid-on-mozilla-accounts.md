---
layout: post
title: Retiring BrowserID on Mozilla Accounts
cover: /assets/img/cover-mozilla.jpg
tags:
- Mozilla
- software
---

The <abbr title="too long; didn't read">tl;dr</abbr> here is that Mozilla
Accounts is turning off SyncStorage BrowserID support and it probably doesn't
affect you at all.


## A little history

In 2011, when Mozilla Accounts (called "Firefox Accounts" back then) was first
built it used BrowserID identity certificates in its authentication model.  The
BrowserID protocol never took off and Mozilla's work on it ended in 2016.
However, the sync service in Firefox continued to use BrowserID even as OAuth
support was added to Mozilla Accounts as an alternative for all other relying
parties.

Over time, we recognized BrowserID was becoming a maintenance liability.  As a
non-standard protocol it created significant complexity in our codebase.
Therefore, we decided to migrate the Firefox clients off of it in favor of
OAuth.

This was an enormous effort, and while much more could be written about this
transition, the main takeaway is that Firefox Sync’s BrowserID support ended
with Firefox 78, which shipped in June 2020 and reached its end of life in
November 2021.

## Present day

We've been waiting a long time for the usage of Firefox 78 to drop.

Aside from being an <abbr title="Extended Support Release">ESR</abbr> version
there are a couple of other reasons for its extra longevity:

- It was the last version of the browser to support Flash
- It was the last version of the browser to support OS X versions < 10.12

With Flash now largely obsolete on the web and traffic from older operating
systems becoming rarer, we’ve decided that now is the appropriate time to turn
off support for this legacy protocol.

To avoid surprises and not leave anyone behind, we attempted to email anyone
still using that endpoint earlier this year. We didn’t receive any feedback and
we continued with the plan.

## Our method

Our plan is simple:  BrowserID requests are the only traffic hitting our
`/v1/certificate/sign` endpoint.  We'll begin returning `HTTP 404` replies to a
small percentage of traffic from that endpoint and monitor for any issues.
Our testing showed no concerns but it's challenging to be comprehensive with so
many combinations of browser versions and operating systems.  Over the next few
weeks we'll continue to ramp up the percentage of 404s until we can remove the
endpoint completely and let the traffic bounce off the front-end like any other
404.

## Current status

Surprise!  I'm a few weeks late with this post.  We started returning 404s on
May 1 and are currently up to ~66% of traffic on that endpoint.  So far there
haven't been any unexpected complications.  We'll continue to increase over the
next few weeks and aim to have all the code removed this summer.
