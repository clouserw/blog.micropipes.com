---
layout: post
title: 10000 commits and going strong
tags:
- Mozilla
- software
---
[Mozilla's SVN repository][1] was started on September 2nd, 2006 and just hit
10000 commits.  That's an average of over 19 commits a day for 520 days
straight!

After my [positive experience with python][2] I was gearing up for a script to
do some repository analysis when I ran across [MPY SVN Stats][3].  After a fast
download and a one line command I had charts and tables full of info.  So,
here's some late night stat work for everyone:

We had a total of 103 people that committed code directly to SVN, 69 of which
had 10 or more commits.  The top 25 committers by total numbers of commits
are:

    No    Author                                Commits    Percentage
    1  	wclouser#mozilla.com                    1558       15.58%
    2 	fligtar#gmail.com                       739        7.39%
    3 	steven#silverorange.com                 707        7.07%
    4 	reed#reedloden.com                      639        6.39%
    5 	pascal.chevrel#mozilla-europe.org       567        5.67%
    6 	fwenzel#mozilla.com                     551        5.51%
    7 	nelson#wordmaster.org                   524        5.24%
    8 	mkaply#us.ibm.com                       481        4.81%
    9 	paul#glaxstar.com                       392        3.92%
    10 	mgalli#mgalli.com                       364        3.64%
    11 	morgamic#mozilla.com                    311        3.11%
    12 	dougt#meer.net                          307        3.07%
    13 	michael.koch#enough.de                  179        1.79%
    14 	ahajdukewycz#mozilla.com                173        1.73%
    15 	shaver#mozilla.com                      162        1.62%
    16 	reed#mozilla.com                        158        1.58%
    17 	abuchanan#mozilla.com                   112        1.12%
    18 	dougt#mozilla.com                       105        1.05%
    19 	eshepherd#mozilla.com                   101        1.01%
    20 	erik#raincitystudios.com                97         0.97%
    21 	mfinkle#mozilla.com                     89         0.89%
    22 	robert#accettura.com                    89         0.89%
    23 	smalolepszy#aviary.pl                   82         0.82%
    24 	oremj#mozilla.com                       76         0.76%
    25 	tim.babych#gmail.com                    58         0.58%

My numbers here (wclouser#mozilla.com) are inflated because I did a lot of the
branching/tagging on our projects.  If you throw my number out as an anomaly
you'll see that no single person has committed more than 7.5% of the code in
SVN.  That's a great community hard at work!

Thanks for all your help!

[1]: http://svn.mozilla.org/
[2]: /2008/01/02/the-most-worthless-bot-on-irc/
[3]: http://mpy-svn-stats.berlios.de/
