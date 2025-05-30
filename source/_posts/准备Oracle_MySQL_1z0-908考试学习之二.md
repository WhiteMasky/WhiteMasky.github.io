---
title: 准备Oracle_MySQL_1z0-908考试学习之二
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-05-27 20:33:39
abbrlink:
---

准备过程中遇到一些问题，发现之前学的关系型数据库的知识和实际实践使用差距太大，我尝试用真题直接刷却发现有太多不明白的知识点，导致背答案都背不下来只能记住选项。但是确实也没有耐心去看完Oracle全程的网课，所以我请ChatGPT给我整理一个简单的大纲，让我能够对数据库有一个基本的概念。这篇是记录我认为其中重要的内容。在了解了基础的SQL语句，ER图以及第x范式之后，这应该可以作为Oracle MySQL学习的很好的开端。

## Overview

- Database Basic
- MySQL Basic
- MySQL Architecture
- SQL Fundamentals
- Datatypes
- Indexes
- Transactions & Locks
- Users & Privileges
- Backup & Restore
- Performance Tuning
- Replication & High Availability
- JSON & New Features



### Database Basic

关系型和非关系型、时间序列、文档，这里我们只关注关系型数据库。RDBMS用行与列组成表，主键与外键将表相连。

SQL是Structured Query Language，是与关系型数据库交互的基本语言，而MySQL是开源的RDBMS。

DBMS的主要功能有数据定义、数据操作、数据安全、并发控制、故障恢复。



### MySQL Basic

MySQL拥有多个核心特点：

- 开源免费 | community版本
- 跨平台 | Win Linux MacOS
- 插件式存储引擎 | InnoDB MyISAM Memory
- 支持事务 | InnoDB支持事务与回滚操作
- 复制与集群 | 主从复制、GTID、高可用架构
- JSON支持
- 优化器支持 | 多种JOIN策略，执行计划分析
- 多用户并发 | 支持读写并发机制，内置锁机制

MySQL的四个版本：

- Community Edition 免费开源
- Enterprise Edition 安全、监控、备份、审计插件
- Cluster 分布式，高可用性，无单点故障，NDB引擎
- HeatWave 与Oracle Cloud集成，OLAP支持

OLAP = Online Analytical Processing

OLTP = Online Transaction Processing



**MySQL Architecture** 见下一部分



**MySQL File System**

- .ibd 数据文件
- .frm 表定义文件（老版本）
- ib_logfile0,ib_logfile1 redo log用于事务恢复
- mysql-bin.* binary log，记录读写操作，可以复制与恢复
- .err 错误日志
- .slowlog 记录缓慢执行sql
- my.cnf / my.ini 数据库参数设置



`SHOW VARIABLES LIKE 'innodb%';`

- innodb_buffer_pool_size 缓冲池大小
- innodb_log_file_size 单个redo文件大小，越大崩溃恢复越慢但性能更高
- innodb_file_per_table 是否为每张单独表创建.ibd，否则都在共享ibdata1
- innodb_flush_log_at_trx_commit redo日志在事务提交时的刷盘行为，影响事务持久性和性能

`0` 每秒刷一次盘，快但不安全

`1` default，每次提交刷一次盘，安全

`2` 中间状态，每次提交写入文件，每秒刷一次，高并发中常用

- innodb_lock_wait_timeout 事务锁等待超时
- innodb_log_buffer_size redo log的缓冲大小
- innodb_flush_method innodb文件刷新方法

`fsync` default

`O_DIRECT` 跳过OS缓存，减少两次缓存，用于SSD



### MySQL Architecture

**Connection Layer**

处理客户端连接，支持线程池机制管理多个

- connection thread 每个连接一个线程
- authentication my.sql表中的信息
- privilege check 验证用户访问表/列的权限
- session variables 每个连接可以有独立变量 如SQL_MODE

------

**SQL Layer** 

Parser SQL转为语法树 → Optimizer 决定执行计划用索引或者全表扫描 → Executor 实际的数据读写和存储引擎有关，默认是InnoDB

- Parser
- Optimizer
  - Index
  - Join Order
  - Nested Loop Join, Hash Join
  - 是否使用临时表，排序方式
- Executor 调用存储引擎API

------

**Storage Engine Layer**

InnoDB 支持事务，支持外键

MyISAM 支持全文索引，速度快，适合读多写少场景

MEMORY 速度快

CSV

ARCHIVE 用于归档，写快但不支持索引



InnoDB 

- 事务ACID 
- 外键支持FK约束 
- 行级锁支持高并发 
- 崩溃恢复Redo&Undo Log支持恢复 
- 聚集索引主键索引即为数据页索引



Redo Log 保证已提交数据不会丢失

Undo Log 用于实现事务的回滚与MVCC

（Multi-Version Concurrency Control， InnoDB 存储引擎实现高并发、快照读、不加锁读的核心机制）

MVCC 多版本并发控制，提升读性能

表空间 存储表和索引的数据文件.ibd 



MyISAM 不支持事务，外键，表级锁（写入时锁住整张表），支持压缩表（支持静态只读数据压缩）



外围组件

`mysqld` MySQL服务守护进程

`mysql` 命令行客户端

`mysqldump` 逻辑备份工具

`mysqladmin` 管理工具，可做重启、状态查看

`mysqlpump` 多线程备份工具



> How a query flows:
>
> 客户端连接 👉 身份验证授权 👉 SQL解析构建语法树 👉 优化器生成执行计划 👉 执行器调用存储引擎读写数据 👉 返回查询结果



### SQL Fundamentals



- DDL
  - CREATE
  - DROP
  - ALTER
  - TRUNCATE
- DML
  - INSERT
  - DELETE
  - UPDATE
- DQL
  - SELECT: WHERE子句，聚合函数，GROUP BY/ HAVING，子查询
- DCL
  - GRANT
  - REVOKE
  - 权限保存在mysql.user mysql.db mysql.tables_priv等表中，检查时按照user@host db table column 顺序



| SQL      | 删除表结构 | 清空表数据 | 是否可恢复 | 是否写入Binlog | 属于哪一种分类 |
| -------- | ---------- | ---------- | ---------- | -------------- | -------------- |
| DROP     | √          | √          | ×          | √              | DDL            |
| TRUNCATE | ×          | √          | ×          | √              | DDL            |
| DELETE   | ×          | 部分或全部 | √          | √              | DML            |



### Data Types

- 数值
  - 整型
  - 浮点型
- 字符串
  - 定长变长
  - 文本
  - 二进制
  - 枚举和集合
- 日期与时间
- JSON
- 空间
- DEFAULT与NULL



### Indexes

有索引可以直接定位，无索引必须全表扫描

InnoDB使用B+树 O(Logn)



- 主键索引
- 唯一索引
- 普通索引
- 复合索引

索引使用时必须放在WHERE子句中，不能使用函数包裹字段，LIKE匹配时要避免开头通配符%abc



`SHOW INDEX FROM users;` 的返回结果也需要了解看懂一下

### Transactions & Locks

ACID Atomic Consistency Isolation Durability

`START TRANSACTION/BEGIN` `COMMIT` `ROLLBACK` `SAVEPOINT` `ROLLBACK TO SAVEPOINT`



InnoDB如何实现事务：

- Redo Log 确保提交的数据不丢失，即使数据库崩溃也能恢复
- Undo Log 记录修改前的版本，可以回滚和MVCC
- Doublewrite Buffer 防止操作系统crash造成部分页写入失败



MySQL支持的隔离级别有：

| 隔离级别         | 出现问题            | 性能 | 默认   |
| ---------------- | ------------------- | ---- | ------ |
| READ UNCOMMITTED | dirty read          | 高   | ×      |
| READ COMMITTED   | non-repeatable read | 中   | Oracle |
| REPEATABLE READ  | Phantom Read        | 低   | MySQL  |
| SERIALIZABLE     | 无并发，安全        | 超低 | ×      |

InnoDB通过MVCC避免了幻读，使用Gap Lock



锁的类型：

| 分类 | 锁类型         | 注释                     |
| ---- | -------------- | ------------------------ |
| 粒度 | table lock     | 读写都锁整张表，MyISAM   |
| 粒度 | row lock       | 读不锁，写锁一行，InnoDB |
| 功能 | shared lock    | 允许读组织写             |
| 功能 | exclusive lock | 只允许自己读写           |

行锁的两种方式：

- record lock 针对记录
- gap lock 针对间隙，避免幻读
- Next-Key Lock (record和gap组合，MySQL default)



### Users & Privileges

MySQL 账号格式

> '用户名'@'主机名'

user: 登录用户名

host: 哪个主机允许连接，localhost，%， IP

关于这一部分的SQL内容大多都在关系型数据库里学过应该



### Backup & Restore

| 备份形式        | 说明                       | 是否影响数据库运行 |
| --------------- | -------------------------- | ------------------ |
| Logical Backup  | 导出SQL语句形式的数据      | 是，有时会锁表     |
| Physical Backup | 复制物理文件，数据页，日志 | 否，可热备         |



`mysqldump` 是MySQL自带的命令行备份工具，用于生成一份含SQL命令的文本文件，可以直接用于恢复。

`mysqlpump` 支持并发导出表。



物理备份一般是停止MySQL服务后直接复制到数据库目录，在Linux中通常是`/var/lib/mysql`，企业有xtrabackup的热备方案。



**Point-in-time Recovery** 

mysqldump全备份 👉 --log-bin记录变更日志 👉 mysqlbinlog重放日志



### Performance Tuning



EXPLAIN分析查询计划



避免慢查询写法，可以用`slow_query_log = 1`(在my.cnf里开启慢查询日志)

- SELECT *
- %abc LIKE
- OR多条件
- 函数包裹字段



| 参数                    | 作用               |
| ----------------------- | ------------------ |
| innodb_buffer_pool_size | 内存缓存中的数据页 |
| query_cache_size        | 已废弃的查询缓存   |
| max_connections         | 最大连接数         |
| thread_cache_size       | 线程重用池         |
| tmp_table_size          | 内存临时表大小     |
| sort_buffer_size        | 排序缓冲区大小     |





### Replication & HA

企业架构的核心，容灾能力和系统扩展性。

Master 异步复制到 Slave

binlog ←←←←←←relay log

- 读写分离：主库负责写，从库负责读；
- 容灾备份：万一主库崩溃了从库可以接上
- 分布式部署：地理分布式数据同步
- 版本迁移：老版本迁移不影响主库



Source            Replica

binlog  → I/O Thread → relay log

​                                  ↓

​                              SQL Thread

**How replication works**

> Master将transaction写入binlog，从库通过I/O Thread读取主库的binlog，写入relay log，slave的SQL thread 读取relay log并执行相同的操作

**How to set up**

> 1. 配置主库my.cnf，然后重启MySQL
>
> 2. 主库创建复制用户
>
> 3. 查看主库位置
>
> 4. 配置从库my.cnf，然后运行命令让从库定位到主库相同位置后，启用从库
>
>    验证是否复制成功 SHOW SLAVE STATUS\G 可以看到 `Slave_IO_Running`和`Slave_SQL_Running` 都 Yes



GTID = Global Transaction ID，全局事务标识符，每个事务都有一个唯一 ID，可跨库唯一标识

配置时主从的my.cnf都要加

- gtid_mode = ON
- enforce-gtid-consistency = ON

而与此同时 `MASTER_LOG_FILE` 和 `POSITION` 就不再需要了



| Type             | Comment                                                   |
| ---------------- | --------------------------------------------------------- |
| asynchronous     | 主库提交后立刻返回，不等待从库，default                   |
| semi-synchronous | 主库需要等待至少一个从库ACK之后才提交，可以升级提升可靠性 |
| synchronous      | 主从全部完成，性能差不推荐                                |



| 类型     | 结构                       | 用途                     |
| -------- | -------------------------- | ------------------------ |
| 单主多从 | 1 Master + N Slaves        | 读写分离                 |
| 主主复制 | Dual Masters               | 双活热备，需要防止写冲突 |
| 多级复制 | Master → Slave 1 → Slave 2 | 地理分布优化             |



HA方案

- MySQL High Availability 自动主从切换，classic
- Group Replication 内置组复制
- MySQL InnoDB Cluster 官方全套HA，多主复制搭配Router使用



### JSON & New Features

JSON支持建立虚拟列索引

虚拟列（这个中文译名不好哇 generated columns一看就知道是根据别的列自动算出来的而非手动）

表分区（物理分一下提升性能）

空间类型 表示地理位置的数据

窗口函数 不分组的情况下进行聚合运算

