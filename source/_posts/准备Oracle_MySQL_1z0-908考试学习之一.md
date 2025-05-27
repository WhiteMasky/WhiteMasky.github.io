---
title: 准备Oracle_MySQL_1z0-908考试学习之一
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-05-20 14:01:17
abbrlink:
---

都是些零碎的知识概念，不成体系的那种，写到哪儿看到哪儿吧

----

**G**lobal **T**ransaction **ID**s **Purged ** **已从当前实例的 binary log 中被彻底删除（PURGE）** 的 GTID 列表。

**“master / slave” 指的是**一组通过 **复制（replication）** 机制保持数据一致的服务器角色：

- Master 接收**写操作**；生成 **Binary Log**（binlog），把每条事务按顺序记录下来。
- Slave 通过网络把 master 的 binlog **拉取并重放**，从而追上数据；可提供**只读查询**或做灾备。

-----

PAM 通过 Linux PAM 模块认证；需把原始口令传给 PAM。

LDAP “Simple Bind” 模式，把口令直接交给 LDAP 服务器。

----

Storage Engine

**存储引擎**负责把表的数据和索引真正落到磁盘（或内存）并实现相应的读写、锁、崩溃恢复等机制。

早年是MyISAM，现在已经更新默认为InnoDB，同时兼容早期版本

通过CREATE_TEMPORARY_TABLE或者ORDER_BY/GROUP_BY命令创建临时表，超过内存阈值时会溢写到磁盘，默认进入#innodb_temp目录，也可以通过innodb_temp_tablespaces_dir指定。

变量tmpdir仍然存在但是只给老机制用，用不到InnoDB



shell中 `grep temp` 输出只会列出文件名或目录名里带 “temp” 的那些条目

**G**lobal **R**egular **E**xpression **P**rint：Linux/Unix 常用的文本搜索命令，用来从输入流或文件中“筛选”出匹配某个模式（pattern）的行。

---

mysqldump是备份/导出命令，mysqlexport早就弃用了

---

logfile group 在 InnoDB 内部把若干 *重做日志文件* 视为一个“组”（由参数控制，无法用 SQL DDL 创建或删除）

---

create-info和TABLE相关，database和DATABASE相关

---

 **“Table I/O Waits Summary”** 表里，`COUNT_*` 列统计的是 **存储引擎对单行（row）的实际处理次数**，而不是 SQL 语句条数，在 InnoDB 里，每删除或读取一行都会触发一次底层 `handler::delete_row()` / `handler::index_read()` 等回调，FETCH/INSERT/UPDATE/DELETE 一行的调用次数，但是`COUNT_READ/WRITE` 则是上面几类的合计（“WRITE” = INSERT + UPDATE + DELETE）

---

index scan 按着primary索引找，table scan是没得索引的时候

---

transient 瞬时的

prolonged 持续的

---

物理升级 (physical/in-place) **保留原 datadir**，仅替换 MySQL 程序文件，再用 `mysql_upgrade`/`mysqlcheck` 修复元数据。

逻辑升级 (logical) 先用 **逻辑备份工具**（`mysqldump` 或 `mysqlpump`）导出 *全部* 数据 → 用新版本创建空实例 → **重新导入** SQL 文件。

---

`gtid_mode=ON log-bin log-slave-updates enforce-gtid-consistency` **重启主从**

 `CHANGE MASTER TO MASTER_AUTO_POSITION = 1` 没有它，从库不会用 GTID 定位主库位置。

---

mysqlcheck

mysqlanalyze

mysqloptimize

myqlrepair

什么命令干什么事

