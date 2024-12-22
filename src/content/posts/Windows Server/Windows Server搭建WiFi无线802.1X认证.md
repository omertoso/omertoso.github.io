---
title: Windows Server搭建WiFi无线802.1X认证
published: 2024-12-22
description: ''
image: ''
tags: [802.1X]
category: Windows Server
draft: false 
lang: ''
---

# 为什么需要Windows Server搭建WiFi无线802.1X认证

在企业网络环境中，使用 **Windows Server 搭建 WiFi 无线 802.1X 认证** 是为了提升无线网络的安全性和管理效率。

#  设备要求

- AP或无线路由器支持 RADIUS认证，可以开启 WPA2-企业/WPA2-Enterprise之类选项

# 部署步骤

1. Raidus 服务器 添加 Active Directory 证书服务、配置 AD CS
   1. mmc 申请 CA 证书
   2. 安装 NPS
   3. NAPS 中网络策略服务器配置
2. AD 服务器 配置网络策略服务器，
   1. 并配置自定义密钥
   2. 添加该组对应的vlan
3. 交换机配置 Raidus

---

参考：

1. [**Windwos Server 2016 实现无线、有线802.1x认证+动态vlan下发**](https://blog.51cto.com/u_11442747/5141964)

2. [使用Windows server搭建WiFi无线802.1X认证](https://zhuanlan.zhihu.com/p/387979923)

3. [部署基于密码的 802.1X 身份验证无线访问](https://learn.microsoft.com/zh-cn/windows-server/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)

   
