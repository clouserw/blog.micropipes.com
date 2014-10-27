---
layout: post
title: Turns out greylisting is awesome
---
I used to get several hundred spam emails a day on micropipes.com.  I wasn't
thrilled with having a four or five digit message count in my spam folder, but I
deleted the few that slipped through each day and didn't think about it much
more.  Someone else running a domain on this server got enough initiative to do
something about it though and installed a [Grey Listing][1] filter.

For those who are unfamiliar, from the site:

> What happen is that each time a given mailbox receives an email from an
> unknown contact (ip), that mail is rejected with a "try again later"-message
> (This happens at the SMTP layer and is transparent to the end user). This, in
> the short run, means that all mail gets delayed at least until the sender
> tries again - but this is where spam loses out! Most spam is not sent out
> using RFC compliant MTAs; the spamming software will not try again later.

It means a short delay to get a message from someone that has never mailed you
before, but subsequent messages are delivered immediately and the amount of spam
I get is nearly nothing now - I'm averaging about one per day.  Definitely a win
if you're fighting a flood of spam.

[1]: http://greylisting.org/
