---
author: "Vonng"
description: "杀查询的正确姿势"
categories: ["PostgreSQL"]
tags: ["PostgreSQL","Admin", "Fault"]
type: "post"
---



# 杀查询的正确姿势



## 相关函数



| Name                             | Return Type | Description                                                  |
| -------------------------------- | ----------- | ------------------------------------------------------------ |
| `pg_cancel_backend(*pid*int)`    | `boolean`   | Cancel a backend's current query. This is also allowed if the calling role is a member of the role whose backend is being canceled or the calling role has been granted `pg_signal_backend`, however only superusers can cancel superuser backends. |
| `pg_reload_conf()`               | `boolean`   | Cause server processes to reload their configuration files   |
| `pg_rotate_logfile()`            | `boolean`   | Rotate server's log file                                     |
| `pg_terminate_backend(*pid*int)` | `boolean`   | Terminate a backend. This is also allowed if the calling role is a member of the role whose backend is being terminated or the calling role has been granted `pg_signal_backend`, however only superusers can terminate superuser backends. |

Each of these functions returns `true` if successful and `false` otherwise.

`pg_cancel_backend` and `pg_terminate_backend` send signals (SIGINT or SIGTERM respectively) to backend processes identified by process ID. The process ID of an active backend can be found from the `pid` column of the `pg_stat_activity` view, or by listing the `postgres` processes on the server (using ps on Unix or the Task Manager on Windows). The role of an active backend can be found from the `usename` column of the`pg_stat_activity` view.



* Psql

```sql
SELECT count(pg_cancel_backend(pid)) FROM pg_stat_activity WHERE application_name !~'psql';
```



* Bash

```bash
sudo -iu postgres /usr/pgsql/bin/psql -qAtzc 'SELECT count(pg_cancel_backend(pid)) FROM pg_stat_activity WHERE application_name !~'"'psql';"
```

