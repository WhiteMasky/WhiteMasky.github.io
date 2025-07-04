---
title: 阿里云ACA扫盲
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-07-04 23:10:58
abbrlink:
---

入职考试要考但是真的一团雾水，最后觉得还是让GPT来救我吧，看课刷题都无从下手，我得先把基本的概念厘清了。ACA = Alibaba Cloud Certified Associate，我们要求掌握的有5个部分：云计算工程师、云原生工程师、云数据库工程师、大数据工程师、大模型工程师。问了GPT推荐的学习顺序是：Cloud Computing （how service deployed on cloud，云平台/XaaS比如IaaS PaaS SaaS/弹性计算/存储/网络），Cloud Database（数据库是云服务特别重要的一环，关系型数据库/NoSQL/大数据存储/RDS/PolarDB），Big Data（how to collect store compute analyze data，MaxCompute/Dataworks/EMR），Cloud Native（Docker/Kubernetes/Microservice/DevOps，如何以原生的方式在云上构建应用），Large Model（AI Model deployment，call，inference，PAI platform，LLM API，knowledge distillation， RAG）

Core Concept：

- Cloud Computing
  - IaaS/PaaS/SaaS
  - ECS
  - OSS
  - VPC
  - 负载均衡SLB 弹性伸缩 自动快照

- Cloud Database

  - Relational Database：MySQL/PostgreSQL
  - RDS 阿里云的数据库托管服务
  - PolarDB兼容MySQL的自研
  - 备份/容灾/只读实例/读写分离

- Big Data

  - MaxCompute  类Hadoop自研大数据计算平台
  - Dataworks 数据开发与调度平台
  - Data Integration 数据采集与同步
  - Hologres 实时分析数据库支持OLAP
  - EMR Elastic MapReduce 大数据生态环境 Spark Hive

  - p.s. 从日志采集 → MaxCompute处理 → 可视化输出 → 使用Hologres做实时查询。

- Cloud Native 
  - 容器 Docker
  - Kubernetes 容器编排
  - 微服务架构
  - Serverless 无需管理服务器按需触发运行
  - DevOps / CI/CD 开发运维一体化
  - p.s. 一个电商系统被拆成订单、支付、推荐3个微服务，分别由容器运行，K8s调度
- LLM
  - PAI 阿里云机器学习平台，支持训练 部署 调用
  - Qwen MaaS
  - 推理服务/在线部署，将模型部署为API服务
  - Prompt Engineering/Knowledge Distillation/RAG检索增强生成