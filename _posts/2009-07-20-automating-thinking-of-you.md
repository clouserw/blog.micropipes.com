---
layout: post
title: Automating "Thinking of you"
tags:
- software
---
<p>I had an idea a few weeks ago.  I've got a bunch of great photos on my computer that no one ever sees unless we meet in person.  Sure, we've got <a href="http://www.flickr.com/">flickr</a> and social networking sites, but I'm talking about an old photo that someone only saw once in passing, or a favorite shot from summer while you're huddled over your heater wondering when the sun is coming back.</p>
<p>I can look at them any time, and there are a few on flickr that other people can look at, but what about people that aren't tech savvy or are really busy and get caught up in the daily grind?</p>
<p>I was thinking, the answer can be a really simple script running from cron, say, weekly.  It picks a random photo from a directory and emails it to a group of people.  That's it.  The idea is:</p>
<ul>
<li>it's low tech compared to RSS feeds and social networking sites.  This "just works" with the tools people (potentially, low-tech people) are already used to using.</li>
<li>in a similar vein, commenting and discussion are built in if you feel like it.</li>
<li>it's focused on the people on the CC list.  Sending out an old photo that is relevant just to those people has a lot more effect than one scrolling by on flickr.  It's got a personal touch.</li>
<li>it's automatic.  You wake up Monday morning, drag yourself to work, and there is a photo from 15 years ago in your inbox and you can laugh about how bad your hair was.  Awesome.</li>
</ul>
<p>So, I thought I would try it and cooked up <a href="https://github.com/clouserw/scripts/blob/master/audreytoo.py">audreytoo</a>.  Basically, you seed a directory with <em>copies</em> of the pictures you want to send out, add the script to a cron job, and it does it's thing.  There are a couple other features in the script that you could look at if you want to get fancier.</p>
<p>I realize there is some irony in using an automated script to say "I'm thinking of you" but as long as I'm on the CC list it's still true. :)  Anyway, I'm sharing the code in case anyone else can find value in it.</p>
