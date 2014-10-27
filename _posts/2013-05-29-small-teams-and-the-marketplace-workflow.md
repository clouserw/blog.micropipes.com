---
layout: post
title: Small teams and the Marketplace workflow
tags:
- Mozilla
---
Towards the end of last year my routine was to find a weeks worth of bugs for
each Marketplace developer, assign what I thought they could do in a week, and
then meet with the person individually to talk about them and make sure we both
thought it was a reasonable amount and the priorities were right.  This worked
fine for smaller teams, however, it's not unusual for us to close 70+ bugs a
week these days and it simply used too much time.  I'd often end up skipping the
folks who were comfortable grabbing bugs on their own, which was fine, but it
didn't encourage discussion within the team of who was working on what and kind
of pushed people into working in isolation.

The last time the whole team was in the same room together (six months ago,
now?) I proposed a new plan which we've been following ever since.  The plan
recognizes that the components within Bugzilla already split the Marketplace
along logical lines (eg. API, Statistics, Reviewer Tools, etc.).  Using those
components as a template I asked everyone what areas they were most interested
in and organized small groups which were responsible for each component.  These
groups meet once a week to do three things for each component:

* Review any new bugs in the component since last time and set priorities.
* Make sure the bugs people are working on are the most appropriate and that
  they are in the current milestone.
* If anyone is blocked on anything either fix it or escalate it.

There are generally only a few new bugs in each component each week so the
meetings are often only a few minutes.  These meetings make discussing current
features a part of the natural development flow instead of making developers go
out of their way to find out what is happening.  If anyone is stuck or confused
it's easy to speak up and get help and it also gives anyone who is interested in
that part of the Marketplace a place to go to ask questions (meetings are open
to anyone).

The main concept behind the plan is that developers are aware of what our goals
and commitments are and know better than I do what needs to be done to get
there.  If I'm in between them and closing bugs I'm just in the way.  This plan
empowers developers to be owners of their components and features and more
officially shares the experience of triaging, prioritizing, and breaking specs
apart into bugs.

I still go to as many of the component meetings as I can and help push things in
the right direction but I have confidence that if I have a conflicting meeting
or am focused on something else I can skip the meeting and there won't be any
critical bugs that don't get addressed.  Using the system has allowed us to add
several more people to the team without having additional layers of management
and still allows me to focus on coordinating with other teams at Mozilla instead
of spending all my time on just the Marketplace team.  Additionally, I still
look at every bug that is filed for the Marketplace, but I'm routinely a couple
days behind on generic bugmail.  If a blocker bug is filed it is usually caught
right away with multiple people watching their components.

The groups aren't set in stone and several people have already switched around.
They are simply a starting point - if nothing else, a bucket of bugs developers
can go to when they have a couple hours to fill and they don't want to spend
their time sorting through our entire list of open bugs.

After several months of using the new system I'm happy to say that it has taken
great strides towards solving the two most common concerns the marketplace team
had:  What are my teammates working on, and what am I working on next
week/month?  Our strategies will continue to evolve as we grow and change but
this has been an effective change for where we are at right now.
