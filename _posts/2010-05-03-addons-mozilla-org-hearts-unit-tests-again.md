---
layout: post
title: addons.mozilla.org ♥s unit tests.  Again.
tags:
- Mozilla
---
[AMO][1] has had an on-again off-again relationship with unit tests.  A little
over a year ago we had [a thousand unit tests][2] that sort of, mostly, ran.
The problem is, PHP unit testing just isn't as good as it should be.  CakePHP
relies on [SimpleTest][3], one of the main PHP test suites.  It worked
relatively well for a small number of tests, but as our suite grew, so did our
troubles.

Our main issue was hitting a memory limit or the max execution time.  We hit the
limits often for a variety of reasons, some legitimate bugs, and some because we
tried to hack around things to make the tests run.  If we change the limits we
affect the tests because they are running within the same environment.  There
wasn't really a concept of fixtures then, although it looks like [CakePHP has
stepped up there][4].  The simple test web runner was hard to use and the mock
objects were sometimes a little too mocked and missing some attributes.

All in all it was a heroic effort to get that many tests, but we didn't maintain
it because they were so slow to write and difficult to run.  Testing can be a
pain to write, sure, but it shouldn't be a burden like that.  Enter [Django's
testing suite][5] (built on top of [Python's unittest][6]).  It has most of our
complaints handled out of the box.  It's very well documented, considers a lot
of aspects of testing, supports fixtures, a built-in client, etc.  It's a well
thought out framework to build tests on.

We're being more vigilant about requiring tests this time around, but they also
aren't as frustrating to write.  When you write them they actually work and they
stay working.  Most of what you want is built in already.  For example, I wrote
the password reset form we needed on AMO in Django.  With CakePHP and SimpleTest
I'd have no idea how to test that the email was actually working.  It's
apparently possible [with a SimpleTest add-on][7] and enough code that I have to
scroll in my browser.  With Django's test suite the actual code was 5 lines, 3
of which were assertions:

{% highlight python %}
def test_request_success(self):
    self.client.post('/en-US/firefox/users/pwreset',
                    {'email': self.user.email})

    eq_(len(mail.outbox), 1)
    assert mail.outbox[0].subject.find('Password reset') == 0
    assert mail.outbox[0].body.find('pwreset/%s' % self.uidb36) > 0
{% endhighlight %}

With the power of the new test suite we're once again writing and maintaining
our unit tests - currently at around 390 tests and increasing steadily.  Plenty
of people have written about why unit tests are important so I won't belabor the
point, but I will mention that it's a great feeling to be able to commit
something and be confident it hasn't affected other parts of the site.  It's
almost as good of a feeling when you write your code and a completely different
test fails pointing out a case that you didn't even consider but one that would
soak up developer time trying to debug down the road.

Building on a foundation that takes testing seriously is great.

[1]: https://addons.mozilla.org
[2]: /blog/2009/04/09/addonsmozillaorg-celebrates-1000-passing-unit-tests/
[3]: http://www.simpletest.org/
[4]: http://bakery.cakephp.org/articles/view/testing-models-with-cakephp-1-2-test-suite
[5]: http://docs.djangoproject.com/en/dev/topics/testing/
[6]: http://docs.python.org/library/unittest.html
[7]: http://www.curioussymbols.com/simplemail/
