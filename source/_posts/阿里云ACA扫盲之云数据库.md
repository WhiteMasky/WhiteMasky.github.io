---
title: 阿里云ACA扫盲之云数据库
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-07-05 14:13:55
abbrlink:
---

| 类型  | 产品                        | 适用                     | 特点                    |
| ----- | --------------------------- | ------------------------ | ----------------------- |
| RDB   | MySQL/PostgreSQL/SQL Server | 有结构的数据 如订单 用户 | 可以SQL查询，用表格组织 |
| NoSQL | MongoDB/HBase/Redis         | 缓存 大数据 非结构化数据 | 灵活/性能高/但弱化事务  |

- RDS 阿里云自动备份、安全加固、高可用性部署，支持MySQL/PostgreSQL/SQL Server/MariaDB
- PolarDB 存储计算分离，支持弹性扩容，比传统RDS快6倍
- Redis 高性能的缓存型数据库，热门数据缓存/秒杀场景/分布式锁



| Concept      | Comment                              |
| ------------ | ------------------------------------ |
| Master-Slave | 一主多从，提升读写能力，防止单点故障 |
| 读写分离     | 主负责写，从负责读                   |
| 自动备份     | 定期快照，支持回滚                   |
| 多可用区部署 | 多个物理位置，容灾能力               |
| 高可用性HA   | 异地热备，秒级切换                   |



安全性设计

- 白名单控制，限制访问IP
- SSL 加密连接
- TDE加密 transparent data encryption
- 漏洞修复、账号权限分离