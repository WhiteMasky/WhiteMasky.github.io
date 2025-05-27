---
title:准备Oracle_MySQL_1z0-908考试学习之二
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
- JSON

### 

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

### MySQL Architecture

**Connection Layer**

处理客户端连接，支持线程池机制管理多个

---

**SQL Layer** 

Parser SQL转为语法树 → Optimizer 决定执行计划用索引或者全表扫描 → Executor 实际的数据读写和存储引擎有关，默认是InnoDB

---

**Storage Engine Layer**

InnoDB 支持事务，支持外键

MyISAM 支持全文索引，速度快，适合读多写少场景

MEMORY 速度快

CSV

ARCHIVE 用于归档，写快但不支持索引



**MySQL File System**

- .ibd 数据文件
- .frm 表定义文件（老版本）
- ib_logfile0,ib_logfile1 redo log用于事务恢复
- mysql-bin.* binary log，记录读写操作，可以复制与恢复
- .err 错误日志
- .slowlog 记录缓慢执行sql
- my.cnf / my.ini 数据库参数设置



`SHOW VARIABLES LIKE 'innodb%';`

- innodb_buffer_pool_size
- innodb_log_file_size
- innodb_file_per_table
- innodb_flush_log_at_trx_commit
- innodb_lock_wait_timeout

### MySQL Architecture







