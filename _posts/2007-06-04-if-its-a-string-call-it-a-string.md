---
layout: post
title: If it's a string, call it a string
tags:
- Mozilla
---
<p>This is probably well documented, but it's a good reminder anyway.  If you've got a column in MySQL that is textual (like a varchar), you need to make sure MySQL sees the data going into it as a string.  Here's an example I stumbled across today when I left out some quotation marks - `averagerating` is a varchar(255):</p>
<div class="code">
<pre>
mysql> select averagerating from addons where id=5001;
+---------------+
| averagerating |
+---------------+
| 0             |
+---------------+
1 row in set (0.00 sec)

mysql> UPDATE addons SET averagerating = 9.33 WHERE id = 5001;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select averagerating from addons where id=5001;
+-----------------------------------------------------+
| averagerating                                       |
+-----------------------------------------------------+
| 9.3300000000000000710542735760100185871124267578125 |
+-----------------------------------------------------+
1 row in set (0.00 sec)

mysql> UPDATE addons SET averagerating = '9.33' WHERE id = 5001;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select averagerating from addons where id=5001;
+---------------+
| averagerating |
+---------------+
| 9.33          |
+---------------+
1 row in set (0.00 sec)
</pre>
</div>
<p>Out of 1131 updates, 67 of them ended up with the extra characters and the rest looked just fine.  That means if you don't double check the data pretty closely, something like this could slip by and lead to trouble later on.  Double check your SQL before you run it!</p>
