---
layout: post
title: The sunset of getpersonas.com
tags:
- Mozilla
---
Over four years ago getpersonas.com was built as a gallery to hold Personas -
easy to make and use themes for Firefox.  A lot of programs were supporting
skins at the time, but I don't know of any which were so simple (literally, move
your mouse over an image on a webpage and it's applied).  A community of artists
formed and many designs emerged - some [amazing and popular][1], some [focused
on specific things][2] (hat tip to CollieSmile), many for sports, or brands, or
just people who wanted pictures of their family in a spot they noticed all day
long.

Honestly, I thought they seemed gimmicky at first, but I started using them
casually and they can be pretty fun.  Every once in a while I'll look up at my
search box and see [this guy][3] and crack a smile and that's enough reason to
keep using them for me.

Now I'm treading down the dangerous path of naming names - a road full of mine
shafts and sharp turns - and if I make a mistake, my apologies, please let me
know or leave a comment.  I wasn't involved at the start of the Personas project
but I think credit for the idea goes to [Chris Beard][4], original add-on
development to [Myk Melez][5], original Firefox development work to the Mozilla
Labs team, [Toby Elliott][6] and [Ryan Doherty][7] as the primary web
developers, [Stephen Donner][8] and [Krupa Raj][9] for QA, and [Jeremy Orem][10]
for IT Support.  I know other teams worked on code here and there, but I think
those were the primary contributors.  I was focused on the engineering
aspects so I'm not sure who to credit for the operational side of things - I
know someone was managing day to day life at the time (it was [Deb
Richardson][11] at some point, and today it's [Amy Tsay][12]) and there were
numerous volunteers reviewing submissions as they came in.  It's probably
worth noting that in all the queues of all the sites at Mozilla the
getpersonas.com queue was the only one I regularly saw completely finished
and empty - kudos to those reviewers.

After seeing the rapid success of Personas we began talking about what we
should do with them.  The site didn't have anyone adding features or doing
maintenance on it - Ryan was the closest person to it and officially he was
working on [AMO][13].  So, after some discussion we decided we would migrate all
the data in getpersonas.com to AMO which would keep all of our themes and
add-ons in one place.  We finished the first steps (relatively) quickly - we
wrote a questionable script which ran periodically and synced Personas listings
from getpersonas.com to AMO.  The files themselves and all the users remained on
getpersonas.com.  Looking purely at the number of times the script finished vs
failed, it did pretty well, but there were times when it would fail constantly
until someone could find time to fix it, much to the concern of the artists who
didn't see new data showing up on AMO.

Meanwhile, our security team decided to add getpersonas.com to the [bug bounty
program][14] which surprised everyone and which we've playfully chided them
about ever since.  Some of our oldest and hacked together code (remember, this
was originally an experiment) was now coming under scrutiny from security
professionals and bored/gifted students from around the world.  Special thanks
to [Matthew Noorenberghe][15] and [Brandon Savage][16] for writing patches to
fight back the flood of incoming security bugs.

A final spur to getting the migration finished came in the form of [Mozilla
Persona][17] - an aptly named identity system, also from our company.  After
some spirited debate it was decided the identity project would use the Persona
name and the personas on getpersonas.com would be referred to as Themes (and the
existing themes we had as Complete Themes).  With all the logistics out of the
way we rapidly adopted the new names everywhere save getpersonas.com which
continued to cling to life.

Late last year [Chris Van Wiemeersch][18] spearheaded a clandestine operation to
finally finish closing down getpersonas.com (with special mention to [Kevin
Ngo][19] for contributing piles of code all the while finishing his final exams,
and Kris Maglione for updating the [Personas Plus add-on][20]).

After another quarter of late nights balancing the migration with developing the
[Firefox Marketplace][21] it's finally happened:  *I'm happy to announce that
getpersonas.com has now officially retired and all the content and artist
accounts have been migrated to AMO.*

It's exciting from a Mozilla point of view because the confusion of projects can
finally end and we can stop pretending to maintain a site that we haven't
actually done anything with for years.  The artists and users have reason to be
happy also, though - moving to AMO means it's on an actively maintained site.
Improvements can happen, [features can be added][22], and new ideas can be
explored.  Finishing this long awaited migration will breathe new life into the
themes community and I'm looking forward to all the fun new ways we'll see
Perso-uhh - I mean - themes, being used.

![A screenshot showing the spike of new users on AMO]({{ site.baseurl }}/assets/img/2013-newusers.png)
A screenshot of new users on AMO on the night we imported the
accounts.  Our usual numbers of 1500/day are eclipsed by 1.5 million that night.
Also a testament to the site's scalability that it didn't miss a beat.

[1]:https://addons.mozilla.org/en-US/firefox/addon/japanese-tattoo/
[2]:https://addons.mozilla.org/en-US/firefox/addon/mozilla-bug-404-hideout/
[3]:https://addons.mozilla.org/en-US/firefox/addon/lolface/
[4]:https://twitter.com/cbeard
[5]:https://twitter.com/mykmelez
[6]:https://twitter.com/tobyelliott
[7]:https://twitter.com/ryandoherty
[8]:https://twitter.com/stephendonner
[9]:https://twitter.com/parijaatha
[10]:https://twitter.com/oremj
[11]:https://twitter.com/dria
[12]:https://twitter.com/catchingamy
[13]:https://addons.mozilla.org/
[14]:http://www.mozilla.org/security/bug-bounty-faq-webapp.html
[15]:http://matthew.noorenberghe.com/
[16]:https://twitter.com/brandonsavage
[17]:http://www.mozilla.org/en-US/persona/
[18]:https://twitter.com/cvanw
[19]:http://ngokevin.com
[20]:https://addons.mozilla.org/en-US/firefox/addon/personas-plus/
[21]:https://marketplace.firefox.com/
[22]:https://blog.mozilla.org/addons/2013/02/28/getpersonas-com-migration-update/
