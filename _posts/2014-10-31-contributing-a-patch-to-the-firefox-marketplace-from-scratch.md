---
layout: post
title: Contributing a patch to the Firefox Marketplace from scratch
tags:
- Mozilla
---

[Jared][1], [Stuart][2], and [Andy][3] recently spent some time focusing on one
of the Marketplace's biggest hurdles for new contributors:  *how do I get all
these moving pieces set up and talking to each other?*

I haven't written a patch for the Marketplace in a while so I decided to see
what all the fuss was about.  First up I, of course, read [the installation
documentation][4].  Ok, I skimmed it, but it looks pretty straight forward.

## Step 1: Install Docker

I'm running Ubuntu so that's as easy as:

`sudo apt-get install docker.io`

To fix permissions (put your own username instead of clouserw):

`sudo usermod -a -G docker clouserw`

## Step 2: Build Dependencies
The steps below had lots of output which I'll skip pasting here, but there were
no errors and it only took a few minutes to run.

{% highlight bash %}
$ git clone https://github.com/mozilla/wharfie
$ cd wharfie

$ bin/mkt whoami clouserw
$ bin/mkt checkout

$ mkvirtualenv wharfie
$ pip install --upgrade pip
$ pip install -r requirements.txt
$ sudo sh -c "echo 127.0.0.1  mp.dev >> /etc/hosts"
{% endhighlight %}

## Step 3: Build and run the Docker containers

I ran this seemingly innocent command:

`$ fig build`

And 9 minutes and a zillion pages of output later I saw a promising message
saying it had successfully built.  One more command:

`$ fig up`

and I loaded http://mp.dev/ in my browser:

![Screenshot of Marketplace](/blog/public/img/docker_marketplace.png)

A weird empty home page, but it's a running version of the Marketplace on my
local computer!  Success!  Although,  I'm not sure it counts unless the unit
tests pass.  Let's see...

{% highlight bash %}
$ CTRL-C  # To shutdown the running fig instance
$ fig run --rm zamboni python ./manage.py test --noinput -s --logging-clear-handlers
[...]
Ran 4223 tests in 955.328s
FAILED (SKIP=26, errors=34, failures=17)
{% endhighlight %}

Hmm...that doesn't seem good.  Apparently there is some work left to get the
tests to pass.  I'll file [bug 1082183][5] and keep moving.  I know Travis-CI
will automatically run all the tests on any pull request so any changes I make
will still be tested -- depending on the changes you make this might be enough.

## Step 4: Let's write some code

If I were new to the Marketplace I'd look at the [Contributing docs][6] and
follow the links there to find a bug to work on.  However, I know [Bug 989121 -
Upgrade django-csp][7] has been assigned to me for six months so I'm going to
do that.

I'll avoid talking about the patch since I'm trying to focus on the *how* and
not the *what* in this post.  The code is all in the /trees/ subdirectory under
wharfie, so I'll go there to write my code.  A summary of the commands:

{% highlight bash %}
$ cd trees/zamboni
$ vi <files>  # Be sure to include unit tests
$ git add <files>
$ git checkout -b 989121  # I name my branches after my bug numbers
$ git commit  # commit messages must include the bug number
$ git push origin 989121
{% endhighlight %}

Now my changes are on Github!  When I load the repository I committed to in my
browser I see a big green button at the top asking if I want to make a pull
request.

![Github pull request button](/blog/public/img/github_pull.png)

I click the button and submit [my pull request][8] which notifies the
Marketplace developers that I'd like to merge the changes in.  It will also
trigger the unit tests and notify me via email if any of them fail.  Assuming
everything passes then I'm all done.

This flow is still a little rough around the edges, but for an adventurous
contributor it's certainly possible.  It looks like [Bug 1011198 - Get a
turn-key marketplace dev-env up and running][9] is tracking progress on making
this easier so if you're interested in contributing feel free to follow along
and jump in when you're comfortable.

[1]: http://jaredkerim.com/
[2]: https://muffinresearch.co.uk/
[3]: http://www.agmweb.ca/
[4]: http://marketplace.readthedocs.org/en/latest/topics/docker.html
[5]: https://bugzilla.mozilla.org/show_bug.cgi?id=1082183
[6]: http://marketplace.readthedocs.org/en/latest/topics/contributing.html
[7]: https://bugzilla.mozilla.org/show_bug.cgi?id=989121
[8]: https://github.com/mozilla/zamboni/pull/2659
[9]: http://bugzil.la/1011198
