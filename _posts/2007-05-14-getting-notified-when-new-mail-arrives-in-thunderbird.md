---
layout: post
title: Getting notified when new mail arrives in Thunderbird
tags:
- Mozilla
---

When writing an extension for Thunderbird, it's a common goal to be able to
tell when new mail has arrived.  In versions of Thunderbird before 2.0, the
accepted practice was to get a pointer to the nsiMsgMailSession and add a
listener that got called when a new mail event happened.  The code would look
something like:

{% highlight javascript %}
  function someListener() { }

  someListener.prototype =
  {
    OnItemAdded: function(parentItem, item) {
        alert('You got mail!');
    }
  }

  var mailSession = Components.classes["@mozilla.org/messenger/services/session;1"].getService(Components.interfaces.nsIMsgMailSession);

  mailSession.AddFolderListener(new someListener(),Components.interfaces.nsIFolderListener.added);
{% endhighlight %}

This code is more verbose than you need (declaring the listener function),
and will get you more events than you need (you'll have to filter the ones you
want in your function).

After researching new methods of being notified for [ThreadBubble][1], I came across
a better method available in Thunderbird 2.0 - using the [nsIMsgFolderNotificationService][2].
If you look at the interface, you can see it distinguishes between an item being
added, deleted, moved, etc.  which makes it easy to pick out the events you want
to watch.

The example above using the new interface looks very similar, but I think it
comes out a lot cleaner:

{% highlight javascript %}
  var someListener = {
      itemAdded: function(item) {
        alert('You got mail!');
      }
  }

  var notificationService = Components.classes["@mozilla.org/messenger/msgnotificationservice;1"].getService(Components.interfaces.nsIMsgFolderNotificationService);

  notificationService.addListener(someListener);
{% endhighlight %}

This method isn't affected by [the bug I mentioned earlier][3], and it's a more direct method of getting notified.

The examples here are sparse on details - you should always be prepared to
catch exceptions from code like this (put it in a try/catch block).  You can see
a complete example in the [ThreadBubble source code][4].


[1]: https://github.com/clouserw/threadbubble
[2]: http://lxr.mozilla.org/mozilla/source/mailnews/base/public/nsIMsgFolderNotificationService.idl
[3]: /2007/05/05/threadbubble-05-released/
[4]: https://github.com/clouserw/threadbubble/blob/master/content/threadbubble.js
