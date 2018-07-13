---
layout: post
title: 'mysql慢查询日志'
date: 2018-7-13
author: sunjialei
tags:  linux ubuntu
---

查看是否开启mysql慢查询日志
```mysql
mysql -u root -p
show variables like '%query%'
```

结果：
```mysql
mysql> show variables like '%query%';
+------------------------------+-------------------------------+
| Variable_name                | Value                         |
+------------------------------+-------------------------------+
| binlog_rows_query_log_events | OFF                           |
| ft_query_expansion_limit     | 20                            |
| have_query_cache             | YES                           |
| long_query_time              | 2.000000                      |
| query_alloc_block_size       | 8192                          |
| query_cache_limit            | 1048576                       |
| query_cache_min_res_unit     | 4096                          |
| query_cache_size             | 16777216                      |
| query_cache_type             | OFF                           |
| query_cache_wlock_invalidate | OFF                           |
| query_prealloc_size          | 8192                          |
| slow_query_log               | OFF                           |
| slow_query_log_file          | /var/log/mysql/mysql-slow.log |
+------------------------------+-------------------------------+
13 rows in set (0.00 sec)
```
其中slow_query_log的值OFF代表没开启慢查询日志,ON的话代表开启了慢查询日志。slow_query_log_file代表慢查询日志存放在什么位置。


开启慢查询日志
```mysql
cd /etc/mysql/mysql.conf.d
sudo vim mysqld.cnf

添加以下参数
slow_query_log = 1
long_query_time = 2
slow_query_log_file = /var/log/mysql/mysql-slow.log
```
其中long_query_time代表记录查询时间超过设置值的sql语句，我这里设置了2s。

保存退出,重启mysql