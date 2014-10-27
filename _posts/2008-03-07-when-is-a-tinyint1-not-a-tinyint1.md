---
layout: post
title: When is a TINYINT(1) not a TINYINT(1)?
tags:
- Mozilla
---
<p>When you're using <a href="http://cakephp.org/">CakePHP</a>!</p>

<p>Turns out CakePHP considers a TINYINT(1) to be a Boolean.  Judging from all
<a href="https://trac.cakephp.org/ticket/1253">the</a> <a
href="https://trac.cakephp.org/ticket/3903">support</a> <a
href="https://trac.cakephp.org/ticket/4026">tickets</a> that have been filed,
I'm not the first person to get taken off guard by this behavior.  When I asked
about it on IRC, the response was that since MySQL considers a TINYINT(1) to be
a Boolean, CakePHP does too.  That's not true.</p>

<p>From the <a href="http://dev.mysql.com/doc/refman/5.0/en/numeric-types.html">MySQL manual</a>:</p>

> As of MySQL 5.0.3, a BIT data type is available for storing bit-field values.
> (Before 5.0.3, MySQL interprets BIT as TINYINT(1).)

<p>That's saying if I request a BIT it will make it a TINYINT, not if I request
a TINYINT it will make it a BIT.  Having a framework change the definitions of
my database columns sounds crazy to me, but judging from <a
href="https://trac.cakephp.org/ticket/1253">the ticket filed in 2006</a> this
has been CakePHP's policy for a long time.  Despite the long standing precedent
I can't find any documentation about it online other than the closing remarks of
those support tickets.  </p>
