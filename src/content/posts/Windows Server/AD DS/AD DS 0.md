---
title: AD（Active Directory）管理（0）
published: 2024-12-12
description: ''
image: ''
tags: [AD DS]
category: Windows Server
draft: false 
---

:::tip
Link
:::

- [Microsoft Search AD](https://learn.microsoft.com/zh-cn/credentials/applied-skills/administer-active-directory-domain-services/)
  - 部署和管理 Active Directory 域服务域控制器
  - 创建和管理 Active Directory 对象
  - 在 Active Directory 中创建和配置组策略对象
  - 管理 Active Directory 中的安全性
  - [引导式项目 - 管理 Active Directory 域服务
- 服务器配置与应用（Windows Server 2008 R2）
- 精通 Windows Server 2016 (第6版)

PDF：https://www.alipan.com/s/KaWppxsSE41
提取码：80co

# What is AD ?

Active Directory（AD）是由微软开发的目录服务，用于Windows域网络。它最初在Windows 2000 Server中引入，现在是Windows Server操作系统的核心功能之一。Active Directory用于**管理和组织网络中的用户、计算机和其他资源，提供身份验证、授权和目录服务**。

# 事件日志路径

```powershell
C:\Windows\System32\winevt\Logs\
```

在这个路径中，会找到以下主要的日志文件：

- **Application.evtx**: 应用程序相关的事件日志。

- **Security.evtx**: 安全相关的事件日志，包括用户登录、文件访问等审计事件。

- **System.evtx**: 系统相关的事件日志，包括系统启动、驱动程序加载等。

- **Setup.evtx**: Windows 安装和更新相关的事件日志。



**1. 审计日志配置**

要启用和查看具体的审计日志（如对象访问、登录失败等），你需要配置 **审计策略**（Audit Policy）：

**2. 启用审计策略**

1. 打开组策略管理控制台**：在服务器上运行 gpedit.msc。**
2. 路径导航**：Computer Configuration > Windows Settings > Security Settings > Advanced Audit Policy Configuration > Logon/Logoff 或 Object Access 等选项。**
3. 启用具体审计项**：例如，启用 “Logon/Logoff” 审计策略来记录用户的登录和注销事件。

**3. 查看审计日志**

要查看审计日志，你可以通过以下方式进行：

- **事件查看器**： 打开 **事件查看器**（Event Viewer），路径如下：

```Power
Control Panel > Administrative Tools > Event Viewer‘
```

然后导航到 **Windows Logs** > **Security** 来查看安全审计日志。

---

参考：

1. [启用系统事件审核日志](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/install/enabling-the-system-event-audit-log)
