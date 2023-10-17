---
layout: post
title: ThreadBubble 0.5 released
tags:
- Mozilla
- software
---

This release fixes an annoying bug that caused messages to disappear from the
message list (even though they were still in the folder).  In previous versions,
if there was a thread with 2 messages in it, and you deleted or moved the root
message, the other would disappear from the display.  If you clicked on a
different folder and came back, the previously nested message would be shown
again.

Fixing this problem was more involved than I was hoping, and while debugging, I
stumbled across what I'm considering a bug in Thunderbird:

If there is a new message in a thread, and I delete the root message, the
OnItemAdded event is fired as if a new message just arrived.  If I delete any
message other than the root, or if there is no message marked "new" in the
thread, the event is not fired.  From my limited understanding of the system, it
seems like OnItemAdded should only be fired when an item is added (either new
mail arrives, or I move a message from another folder).  Regardless, I'm no
longer using the OnItemAdded hook, so it's not an issue for ThreadBubble any
more.

It's also worth noting that ThreadBubble now only works with Thunderbird version
2.0 and above due to the way it gets notified about new mail.

[Download ThreadBubble 0.5](https://github.com/clouserw/threadbubble)
