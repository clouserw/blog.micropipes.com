---
layout: post
title: SQLite more laid back than the D-O-double-G
---
<p>SQLite only supports a <a href="http://www.sqlite.org/datatype3.html">simple set of data types</a> and the only one that really matters is "INTEGER PRIMARY KEY" so you can have it auto-increment.  In fact, by default, I can declare the columns as anything I want and it doesn't even throw a warning.</p>
<pre><code>
sqlite> CREATE TABLE t2(c1 wtf, c2 yomama);
sqlite> INSERT INTO t2 VALUES(1, 'blah');
sqlite> SELECT * FROM t2;
1, blah
</code></pre>
<p>This is all documented and explained so I can't complain to much but it's still an interesting concept.</p>
