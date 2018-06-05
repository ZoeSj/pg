---
author: "Vonng"
description: "清理template0"
categories: ["PostgreSQL"]
tags: ["PostgreSQL","Admin", "Fault"]
type: "draft"
---



# template0老化

模板数据库 `template0` 默认是不接受连接的，一般也不会出现要清理的问题。

但有时候因为一些==**未知的原因**==，它的年龄也会飚高，这就需要注意了。



修改`pg_database`系统表中的`datallowconn`字段，就可以修改`template0`的连接属性，连上去`vacuum`了。

使用以下脚本进行治疗：

```bash
#!/bin/bash

# print
psql -qAtc "select datname,age(datfrozenxid) FROM pg_database where datname ~ 'template';"

# fix postgres
psql -qAtc "VACUUM FREEZE;"
psql template1 -qAtc "VACUUM FREEZE;"


psql -tc "update pg_database set datallowconn='t' where datname='template0';"
psql template0 -qAtc "VACUUM FREEZE;"
psql -tc "update pg_database set datallowconn='f' where datname='template0';"

# print
psql -tc "select datname,age(datfrozenxid) FROM pg_database;"

```



## 教训

* 监控的时候不能只盯着一个目标数据库的年龄
* 所有数据库的age都需要纳入监测，因为不知道什么时候就会有惊喜。