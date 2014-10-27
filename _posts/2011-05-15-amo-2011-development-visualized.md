---
layout: post
title: AMO 2011 Development Visualized
tags:
- Mozilla
---
<p>I was playing around with <a href="http://code.google.com/p/gource/">gource</a> this weekend while watching the <a href="http://www.pokerstrategytsl3.com/">TSL 3 Finals</a> and pointed it at <a href="https://github.com/jbalogh/zamboni">addons.mozilla.org's source repository</a>.  I sped it up to display 1 day of commits per second and piped it all to ffmpeg to make a video.  </p>
<p>It turned out pretty well so here is addons.mozilla.org development so far for 2011 (in HD!):</p>
<p><video width="1280" height="720" controls preload="none"><br />
    <source src="http://people.mozilla.org/~clouserw/public/blog/amo-2011-development.ogv" type='video/ogg; codecs="theora"'><br />
</video><br />
(Warning: prefetching is off but if you click play you're in for an 80MB video.)</p>
<p>The gource docs are easy to read if you want to do this for your project, but for the record this is what I ran:<br />
<code><br />
gource --viewport 1280x720 \<br />
       --user-image-dir ~/sandbox/zamboni/.git/avatar/ \<br />
       --title "addons.mozilla.org" \<br />
       --auto-skip-seconds 1 \<br />
       --seconds-per-day 1 \<br />
       --start-position .715 \<br />
       --max-file-lag 0.5 \<br />
       --max-files 5000 \<br />
       --camera-mode track \<br />
       -o -<br />
</code></p>
<p>Piped to:<br />
<code><br />
ffmpeg -y \<br />
       -r 60 \<br />
       -f image2pipe \<br />
       -vcodec ppm \<br />
       -i - \<br />
       -vcodec libtheora \<br />
       -b 10000K \<br />
       ~/out.ogv<br />
</code></p>
<p>That gave me a 180MB uncompressed ogv.  The uncompressed version looks far nicer, but that's a lot of bandwidth for a random video so I cut it down with ffmpeg2thoerea (anyone know the switch to do this directly in the ffmpeg command?):<br />
<code><br />
ffmpeg2theora -v 4<br />
              ~/out.ogv<br />
              --optimize<br />
              --noaudio<br />
              -o amo-2011-development.ogv<br />
</code></p>
