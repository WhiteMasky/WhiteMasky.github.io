---
title: 阿里云ACA扫盲之大数据
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-07-05 14:53:48
abbrlink:
---

BigData = Volume Velocity Variety Value

体量大（TB PB） 处理快（需要实时或者准实时处理）类型多（非结构化/半结构化/结构化）价值密度低（大量数据中提炼信息）

| 产品             | 作用                 | 备注                                      |
| ---------------- | -------------------- | ----------------------------------------- |
| MaxCompute       | 分布式大数据计算平台 | 类Hadoop，支持SQL/Python                  |
| DataWorks        | 数据开发 调度平台    | 数开主要使用                              |
| E-MapReduce      | 原生Hadoop环境       | 适合复杂Spark/Hive作业                    |
| Hologres         | 实时数据分析数据库   | OLAP分析场景                              |
| Data Integration | 数据同步工具         | 把数据从源搬到目标比如从RDS搬到MaxCompute |
| QuicBI / DataV   | 数据可视化           | 结果展现                                  |

数仓建模流程 ETL

-  Extract
  - 数据源：日志/MySQL/Redis/OSS
  - 工具： Data Integration，DataHub
- Transform
  - 清洗无效字段，统一格式，聚合计算
  - 工具： MaxCompute SQL, Dataworks任务
- Load
  - 将加工后数据写入目标数据库，如MaxCompute/Hologres



打开这些产品看一看吧 Hadoop， Kafka， Spark， Hive

MaxCompute， DataWorks， EMR， Hologres， Data Integration， QuickBI/DataV， Flink， Tableau