---
title: MySQL性能优化（一）
date: 2019-07-14 02:06:13
tags:
 - MySQL
---

# MySQL性能优化（一）

## 1、MySQL现状

MySQL 应该是最流行的 Web 后端数据库。WEB 开发语言近期发展非常快，PHP， Ruby, Python, Java 各有特点，尽管 NoSQL 近期越來越多的被提到，可是相信大部分架构师还是会选择 MySQL 来做数据存储。

MySQL 如此方便和稳定。但是我们在开发 WEB应用程序的时候非常少想到它。即使想到，优化也是程序级别的。比方，不要写过于消耗资源的 SQL 语句。可是除此之外，在整个系统上仍然有非常多能够优化的地方。

## 2、优化策略

### 选择合适的存储引擎

除非你的数据表仅仅用来读或者是全文检索，那是MySQL存储引擎MyISAM的长处（相信如今提到全文检索，没人会用MyISAM存储引擎）。你应该默认选择InnoDB存储引擎。

你自己在测试的时候可能会发现MyISAM存储引擎比InnoDB速度快。这是由于MyISAM仅仅缓存索引。而InnoDB缓存数据和索引，MyISAM不支持事务。可是假如你使用 innodb_flush_log_at_trx_commit=2 能够获得接近MyISAM的读取性能（相差百倍）。

#### 怎样把现有数据库存储引擎MyISAM修改为InnoDB？

```mysql
ALTER TABLE {tableName} ENGINE=InnoDB;
```

为每一个表分别创建InnoDB File：

```mysql
innodb_file_per_table=1
```

这样能够保证 ibdata1 文件不会过大。失去控制。尤其是在运行 mysqlcheck -o –all-databases 的时候。

### 保证从内存中读取数据，将数据保存在内存中

#### 设置足够大的innodb_buffer_pool_size

##### 什么是innodb buffer pool（InnoDB缓存池）？

##### InnoDB buffer pool里包含什么？

##### innodb_buffer_pool_size的取值

##### innodb_buffer_pool_size配置示例

##### 在线调整InnoDB缓冲池大小

##### 监控在线缓冲池调整进度



