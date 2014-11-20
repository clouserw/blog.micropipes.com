---
layout: post
title: Altering large tables without bringing down your service
tags:
- Mozilla
---

When we run *ALTER* statements on our big tables we have to plan ahead to keep
from breaking whatever service is using the database.  In MySQL, many times\* a
simple change to a column (say, from being a short varchar to being a text
field) can read-lock the entire table for however long it takes to make the
change.  If you have a service using the table when you begin the query you'll
start eating into your downtime budget.

If you have a large enough site to have database slaves you'll have a
double-whammy - all reads will block on the master altering the table, and then,
by default, the change will be replicated out to your slaves and not only will
they read-lock the table while they alter it, but they will pause any further
replication until the change is done, potentially adding many more hours of
outdated data being returned to your service as the replication catches up.

The good news is, in some situations, we can take advantage of having database
slaves to keep the site at 100% uptime while we make time consuming changes to
the table structure.  The notes below assume a single master with multiple
independent slaves (meaning, the slaves aren't replicating to each other).

Firstly, it should go without saying, but the client application needs to
gracefully handle both the existing structure and the anticipated structure.

When you're ready to begin, pull a slave out of rotation and run your alter
statement on it.  When it completes, put the slave back into the cluster and let
it catch up on replication.  Repeat those steps for each slave.  Then failover
one of the slaves as a new master and pull the old master out of rotation and
run the alter statement on it.  Once it has finished put it back in the cluster
as a slave.  When the replication catches up you can promote it back to the
master and switch the temporary master back to a slave.

At this point you should have the modified table structure everywhere and be
back to your original cluster configuration.

*Special thanks to [Sheeri][1] who explained how to do all
the above and saved us from temporarily incapacitating our service.*

\*What changes will lock a table vary depending on the version of MySQL.  Look
for "Allows concurrent DML?" [in the table on this manual page][2].

[1]: http://www.sheeri.com/
[2]: http://dev.mysql.com/doc/refman/5.6/en/innodb-create-index-overview.html
