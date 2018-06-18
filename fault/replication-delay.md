# 复制延迟问题



通常复制延迟在几k到百来k都算是正常的。但有时候可能会非常结果可能会……

![image-20180613125041403](checkpoint-repl-delay.assets/image-20180613125041403.png)

![image-20180606082451691](replication-delay.assets/image-20180606082451691.png)



```
2018-06-13 06:22:03.743 CST,,,87224,,5952b191.154b8,20165,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 07:06:34.532 CST,,,87224,,5952b191.154b8,20166,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint complete: wrote 588028 buffers (12.5%); 0 transaction log file(s) added, 0 removed, 2939 recycled; write=2638.446 s, sync=0.573 s, total=2670.789 s; sync files=7873, longest=0.055 s, average=0.000 s",,,,,,,,,""
2018-06-13 07:12:03.670 CST,,,87224,,5952b191.154b8,20167,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 07:47:03.121 CST,,,111197,,5b205b76.1b25d,1,,2018-06-13 07:47:02 CST,23/3494056819,0,LOG,55P03,"skipping vacuum of ""user_counters"" --- lock not available",,,,,,,,,""
2018-06-13 07:47:04.471 CST,"postgres","putong-shard",38517,"[local]",5b203451.9675,1,"",2018-06-13 05:00:01 CST,18/0,0,LOG,00000,"duration: 10023231.667 ms  statement: VACUUM FREEZE VERBOSE;",,,,,,,,,"psql"
2018-06-13 07:53:33.926 CST,,,87224,,5952b191.154b8,20168,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint complete: wrote 1762869 buffers (37.4%); 0 transaction log file(s) added, 0 removed, 3175 recycled; write=2454.520 s, sync=0.526 s, total=2490.255 s; sync files=3738, longest=0.052 s, average=0.000 s",,,,,,,,,""
2018-06-13 08:02:04.069 CST,,,87224,,5952b191.154b8,20169,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 08:32:44.629 CST,"postgres","putong-shard",38517,"[local]",5b203451.9675,2,"",2018-06-13 05:00:01 CST,18/0,0,LOG,00000,"duration: 2740152.144 ms  statement: ANALYZE VERBOSE;",,,,,,,,,"psql"
2018-06-13 08:37:06.180 CST,,,87224,,5952b191.154b8,20170,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint complete: wrote 2081225 buffers (44.1%); 0 transaction log file(s) added, 0 removed, 1107 recycled; write=2089.588 s, sync=0.348 s, total=2102.110 s; sync files=3496, longest=0.060 s, average=0.000 s",,,,,,,,,""
2018-06-13 08:52:04.294 CST,,,87224,,5952b191.154b8,20171,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 09:28:29.197 CST,,,87224,,5952b191.154b8,20172,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint complete: wrote 2197130 buffers (46.6%); 0 transaction log file(s) added, 0 removed, 1309 recycled; write=2169.975 s, sync=0.376 s, total=2184.902 s; sync files=3398, longest=0.050 s, average=0.000 s",,,,,,,,,""
2018-06-13 09:42:04.328 CST,,,87224,,5952b191.154b8,20173,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 10:18:32.694 CST,,,87224,,5952b191.154b8,20174,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint complete: wrote 2231983 buffers (47.3%); 0 transaction log file(s) added, 0 removed, 1459 recycled; write=2171.460 s, sync=0.467 s, total=2188.365 s; sync files=3361, longest=0.072 s, average=0.000 s",,,,,,,,,""
2018-06-13 10:32:04.832 CST,,,87224,,5952b191.154b8,20175,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 11:07:52.349 CST,,,87224,,5952b191.154b8,20176,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint complete: wrote 2267224 buffers (48.0%); 0 transaction log file(s) added, 0 removed, 1634 recycled; write=2129.058 s, sync=0.364 s, total=2147.517 s; sync files=3372, longest=0.038 s, average=0.000 s",,,,,,,,,""
2018-06-13 11:22:04.497 CST,,,87224,,5952b191.154b8,20177,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 11:56:54.663 CST,,,87224,,5952b191.154b8,20178,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint complete: wrote 2294846 buffers (48.6%); 0 transaction log file(s) added, 0 removed, 1827 recycled; write=2069.464 s, sync=0.453 s, total=2090.166 s; sync files=3401, longest=0.038 s, average=0.000 s",,,,,,,,,""
2018-06-13 12:01:34.187 CST,"putong","putong-shard",46433,"10.191.160.10:36072",5b20971e.b561,1,"",2018-06-13 12:01:34 CST,7/70482962,0,FATAL,28P01,"password authentication failed for user ""putong""","Connection matched pg_hba.conf line 8: ""host  all all 10.191.160.0/20 md5""",,,,,,,,""
2018-06-13 12:10:31.829 CST,"putong","putong-shard",62637,"10.191.160.10:36304",5b209917.f4ad,1,"",2018-06-13 12:09:59 CST,2/2847007559,0,ERROR,42P01,"relation ""rel_8192_2552.user_counters"" does not exist",,,,,,"select * from rel_8192_2552.user_counters where user_id=158009848;",15,,""
2018-06-13 12:12:04.821 CST,,,87224,,5952b191.154b8,20179,,2017-06-28 03:27:13 CST,,0,LOG,00000,"checkpoint starting: time",,,,,,,,,""
2018-06-13 12:23:36.122 CST,,,87220,,5952b190.154b4,30,,2017-06-28 03:27:12 CST,,0,LOG,00000,"received SIGHUP, reloading configuration files",,,,,,,,,""
```



07:53:06

