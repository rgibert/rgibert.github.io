---
title: Show PostgreSQL Vacuum Process
tags:
    - db
    - postgresql
---

# Show PostgreSQL Vacuum Process

~~~ sql
SELECT 100.0 * heap_blks_scanned / heap_blks_total
FROM pg_stat_progress_vacuum vac
JOIN pg_stat_user_tables ut
ON (vac.relid = ut.relid)
WHERE relname = $table
~~~
