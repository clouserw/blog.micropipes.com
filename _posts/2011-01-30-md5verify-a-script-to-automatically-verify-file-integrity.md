---
layout: post
title: 'md5verify: A script to automatically verify file integrity'
tags:
- software
---
<p>I have a lot of files on my computer.  Email archives, personal documents, stuff for work, photos I've taken...the list goes on - I'm sure most people reading this are in a similar boat.  On occasion I've found some files to be missing or corrupt which is disturbing but is probably something to be expected.  The bad part is, I keep backups, but I rotate them out when they reach a certain age which means if I don't notice a file is corrupt or missing I'll eventually lose it forever.</p>
<p>I stayed up late a few nights ago and wrote <a href="http://github.com/clouserw/scripts/blob/master/md5verify.py">a script to raise an alert when something has changed</a>.  On its first run the script will recursively walk a directory tree hashing each file and storing the hashes in the directory (in an md5sum compatible formatted file).  On subsequent runs it will begin tracking new files automatically but it will also print messages for missing and changed files.  By saving the checksums in each directory it becomes portable - you can copy a directory somewhere else and still be able to verify nothing changed (a quick <em>md5sum -c checksums.txt</em> will let you know).</p>
<p>By default the script only prints messages when it sees something fishy so it's perfect to drop into cron and it uses exit statuses so it'll work for nagios too.  I've been running it for a few months and have found a couple files that have changed - nothing critical yet but it's nice to know it's there.</p>
