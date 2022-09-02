---
title: List PostgreSQL Vacuum Proccesses With Table Names
tags:
    - db
    - postgresql
---

# List PostgreSQL Vacuum Proccesses With Table Names

~~~ sql
SELECT ut.relname, vac.*
FROM pg_stat_progress_vacuum vac
JOIN pg_stat_user_tables ut
ON (vac.relid = ut.relid);
~~~
