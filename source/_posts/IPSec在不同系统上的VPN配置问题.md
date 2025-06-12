---
title: IPSec在不同系统上的VPN配置问题
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-06-11 17:22:32
abbrlink:
---





之前一直时买机场，最近收到了朋友自己搭的梯子，使用的是L2TP/IPSec，预共享密钥的方式。发现自己第一次用非傻瓜式的还是有点不会，得学计算机网络了。费了老大劲儿里把iOS/Android/Windows三台机器配完，just记录一下步骤。

收到的配置信息如下：

- `Server IP`
- `IPSec PSK`
- `Username`
- `Password`

### iOS

从 `Settings` 进去到 `VPN` 然后 `Add VPN Configuration` 

- **Type**选 `IPSec` ，出来会看见CISCO思科的图标
- **Description** 自己选个喜欢的名字
- **Server** `ServerIP`
- **Account** `Usrname`
- **Password** `Password`
- **Use Certificate** 不开启
- **Group Name** 留空
- **Secret** `IPSec PSK`
- **Proxy** OFF 



### Windows

从 `设置` 到 `网络和Internet` 可以看到 `VPN`，然后 `添加VPN`。

- **连接名称** 起名儿
- **服务器名称或地址** `Server IP`
- **VPN类型** `使用预共享密钥的L2TP/IPSec`
- **预共享密钥** `IPSec PSK`
- **登录信息的类型** `用户名和密码`
- **用户名** `Username`
- **密码** `Password` 

除此以外，还要修改注册表让Windows连接在防火墙之后L2TP/IPSec协议VPN，参考[Microsoft Learn](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/configure-l2tp-ipsec-server-behind-nat-t-device)

> 注册表里找到 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PolicyAgent
>
> 新建 DWORD (32位)值 ： 名称：AssumeUDPEncapsulationContextOnSendRule，数据：2 
>
> 重启系统



### Android

我的vivo手机在不安全的连接里设置来设置去暂时还没找到解决办法，strongswan也不会用，还得再研究下