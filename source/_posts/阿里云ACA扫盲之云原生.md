---
title: 阿里云ACA扫盲之云原生
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-07-05 16:37:34
abbrlink:
---

Cloud Native是一种利用云计算优势来构建和运行应用的方法

核心理念：弹性扩展，自动化部署，快速迭代，容器化，微服务

| 技术         | 作用                 | Ali Cloud          |
| ------------ | -------------------- | ------------------ |
| Docker       | 应用及其依赖打包     | 镜像服务ACR        |
| Kubernetes   | 管理和调度大容器     | 容器服务ACK        |
| Microservice | 拆分应用成小服务     | 微服务引擎MSE      |
| Service Mesh | 微服务之间的流量治理 | ASM 阿里云服务网格 |
| Serverless   | 函数触发，按需运行   | 函数计算FC         |
| DevOps       | 开发运维一体化       | CodePipeline, EDAS |



单体架构 所有功能打包部署 开发快，难维护

微服务架构 每个功能独立运行 部署复杂但易扩展

serverless架构 事件触发函数运行 灵活适合轻量任务