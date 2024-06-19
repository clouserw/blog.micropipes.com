---
layout: post
title: Using Borg on TrueNAS
cover: /assets/img/cover-hack.jpg
tags:
- software
- walkthrough
---

I installed TrueNAS a couple months ago to try out ZFS.  It has some simple
backup options built-in but I didn't see any encrypted options.  Since I use
[Borg](https://www.borgbackup.org/) elsewhere I thought this was a good
opportunity to figure out how to put it on TrueNAS. TrueNAS is based on Debian,
but relying on direct package installations isn't recommended so I needed
another option.

I was going to use [TrueCharts' borg chart](https://truecharts.org/charts/stable/borg-server/) but TrueNAS SCALE is
[phasing out support for charts completely](https://forums.truenas.com/t/the-future-of-electric-eel-and-apps/5409/7)
so I opted to install a binary manually and see if a standard approach appears
later.  It turned out to be pretty straight forward, steps below:

1. Download a [borg binary](https://github.com/borgbackup/borg/releases).
   You'll want to use a version of the unfortunately-named `borg-linuxnewer64`
   builds which are built for Debian 12.  I used the latest stable version,
   `1.2.8`.
2. Copy the binary somewhere.  I put it in `/mnt/bin/`.
3. Try to run `/mnt/bin/borg -V`.  If you get an error saying
   `/mnt/bin/borg: error while loading shared libraries: libz.so.1: failed to
   map segment from shared object` you need to add a temp directory it can
   write to.  I made `/mnt/tmp` and then ran `export TMPDIR="/mnt/tmp"`.

Now `/mnt/bin/borg -V` should work and you can add it to whatever scripts you
use to backup your system.  Don't forget to set the TMPDIR in your scripts too.
