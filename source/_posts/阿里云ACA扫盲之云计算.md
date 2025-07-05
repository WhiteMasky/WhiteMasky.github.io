---
title: 阿里云ACA扫盲之云计算
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-07-05 13:46:32
abbrlink:
---

云计算是按需提供计算资源（服务器存储数据库网络etc.)

| 模型 | 用户                 | 产品                |
| ---- | -------------------- | ------------------- |
| IaaS | 自己装系统，自己部署 | ECS OSS VPC         |
| PaaS | 云平台搭好运行环境   | PAI FunctionCompute |
| SaaS | 云平台提供完整应用   | DataV 钉钉 企业邮箱 |

- ECS Elastic Compute Service 云服务器，租用的Win或Linux虚拟机

- OSS Object Storage Service 对象存储，用于放大文件，无限容量

- SLB Server Load Balance 将流量分发给多个ECS，提高可用性

- VPC Virtual Private Cloud 让云资源安全通信，可以设置防火墙 子网 NAT

- AS Auto Scaling 根据访问自动调节ECS实例，降本

- SG Security Group 类似防火墙，控制哪些IP/端口可以访问ECS

> 云计算的优势有 快速部署/节约成本/弹性伸缩/安全合规/全球可用

镜像：已经预装好系统和软件的模板

实例：已经启动的ECS

快照：类似备份，可回滚

公网IP：互联网上可以访问的IP

弹性公网IP（EIP）：独立的IP可以绑定多个ECS

NAT网关：内网访问公网/公网访问内网的桥梁

云助手：批量管理ECS的运维工具