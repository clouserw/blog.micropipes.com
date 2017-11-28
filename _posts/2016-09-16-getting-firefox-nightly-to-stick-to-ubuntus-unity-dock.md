---
layout: post
title: Getting Firefox Nightly to stick to Ubuntu's Unity Dock
tags:
- Mozilla
---

I installed Ubuntu 16.04.1 this week and decided to try out Unity, the default
window manager.  After I installed Nightly I assumed it would be simple to get
the icon to stay in the dock, but Unity seemed confused about Nightly vs the
built-in Firefox (I assume because the executables have the same name).

It took some doing to get Nightly to stick to the Dock with its own icon.  I
retraced my steps and wrote them down below.

My goal was to be able to run a couple versions of Firefox with several
profiles.  I thought the easiest way to accomplish that would be to add a new
icon for each version+profile combination and a single left click on the
icon would run the profile I want.

After some research, I think the Unity way is to have a single icon for each
version of Firefox, and then add `Actions` to it so you can right click on the
icon and launch a specific profile from there.

Installing Nightly
------------------
If you don't have Nighly yet, [download Nightly][1] (these steps should work fine with Aurora or Beta
also).  Open a terminal:

```bash
$ mkdir /opt/firefox
$ tar -xvjf ~/Downloads/firefox-51.0a1.en-US.linux-x86_64.tar.bz2 /opt
```

You may need to `chown` some directories to get that in `/opt` which is fine.
At the end of the day, make sure your regular user can write to the directory or
else you won't be able to install Nightly's updates.

Adding the icon to the dock
---------------------------

Then create a file in your home directory named `nightly.desktop` and paste this
into it:

```ini
[Desktop Entry]
Version=1.0
Name=Nightly
Comment=Browse the World Wide Web
Icon=/opt/firefox/browser/chrome/icons/default/default128.png
Exec=/opt/firefox/firefox %u
Terminal=false
Type=Application
Categories=Network;WebBrowser;
Actions=Default;Mozilla;ProfileManager;

[Desktop Action Default]
Name=Default Profile
Exec=/opt/firefox/firefox --no-remote -P minefield-default

[Desktop Action Mozilla]
Name=Mozilla Profile
Exec=/opt/firefox/firefox --no-remote -P minefield-mozilla

[Desktop Action ProfileManager]
Name=Profile Manager
Exec=/opt/firefox/firefox --no-remote --profile-manager
```

Adjust anything that looks like it should change, the main callout being the
`Exec` line should have the names of the profiles you want to use (in the above
file mine are called `minefield-default` and `minefield-mozilla`).  If you have
more profiles just make more copies of that section and name them appropriately.

If you think you've got it, run this command:

```bash
  $ desktop-file-validate nightly.desktop
```

No output?  Great -- it passed the validator.  Now install it:

```bash
  $ desktop-file-install --dir=.local/share/applications nightly.desktop
```

Two notes on this command:

  1. If you leave off --dir it will write to `/usr/share/applications/` and
     affect all users of the computer.  You'll probably need to `sudo` the
     command if you want that.
  2. Something is weird with the parsing.  Originally I passed in
     `--dir=~/.local/...` and it literally made a directory named `~` in my home
     directory, so, if the menu isn't updating, double check the file is getting
     copied to the right spot.

Some people report having to run `unity` again to get the change to appear, but
it showed up for me.  Now left-clicking runs Nightly and right-clicking opens a
menu asking me which profile I want to use.

<img src="/blog/public/img/2016-nightly-on-unity.png" title="Screenshot of the right-click menu." />

Modifying the Firefox Launcher
------------------------------

I also wanted to launch profiles off the regular Firefox icon in the same way.

The easiest way to do that is to copy the built-in one from
`/usr/share/applications/firefox.desktop` and modify it to suit you.
Conveniently, Unity will override a system-wide .desktop file if you have one
with the same name in your local directory so installing it with the same
commands as you did for Nightly will work fine.

Postscript
----------

I should probably add a disclaimer that I've used Unity for all of two days and there
may be a smoother way to do this.  I saw a couple of 3rd-party programs that
will generate .desktop files but I didn't want to install more things I'd rarely
use.  Please leave a comment if I'm way off on these instructions! :)

[1]:https://nightly.mozilla.org/

Updated 2017-11-27: I updated the icon path above.  Thanks to kus for the
comment.
