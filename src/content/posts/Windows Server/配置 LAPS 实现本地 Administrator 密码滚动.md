---
title: 配置 LAPS 实现本地 Administrator 密码滚动
published: 2024-12-22
description: ''
image: ''
tags: [LAPS]
category: Windows Server
draft: false 
---

# LAPS

WindowsLAPS是微软的一项新功能，用于自动管理和备份Windows系统本地管理员账户的密码，现原生集成到Windows操作系统中，加强了与AzureAD的协作。该功能支持密码滚动，强化了安全性，并可通过Azure和Intune进行管理。企业可以使用LAPS提升其域环境的安全性。

通过 **Windows LAPS**，可以实现本地管理员账户密码的自动轮换和集中化管理，从而获得以下关键安全和管理优势：

1. **防御攻击：** 有效防范传递哈希和横向遍历攻击。
2. **提升安全性：** 提高远程帮助台支持场景下的安全性。
3. **设备恢复：** 在设备无法访问时，支持通过本地管理员账户登录和恢复。
4. **精细化安全控制：** • 使用访问控制列表 (ACL) 和可选密码加密机制，保护存储在 **Windows Server Active Directory** 中的密码。 • 支持基于 **Microsoft Entra ID** 角色的访问控制模型，确保对存储在云中的密码的保护。
5. **兼容性支持：** 提供与旧版 Microsoft LAPS 的兼容性，便于迁移和升级。

## Windows LAPS 的关键使用场景

您可以在以下场景中部署和使用 **Windows LAPS**：

**1. 备份到 Microsoft Entra ID**

适用于加入 **Microsoft Entra ID** 的设备，自动备份和管理本地管理员账户密码，并应用基于 **Entra** 的访问控制。

**2. 备份到 Windows Server Active Directory**

适用于已加入 **Windows Server Active Directory** 的客户端和服务器，集中备份和管理本地管理员账户密码。

**3. DSRM 帐户密码管理**

为 **Windows Server Active Directory** 域控制器提供目录服务还原模式 (DSRM) 帐户密码的自动备份和集中管理。

**4. 兼容旧版 Microsoft LAPS**

延续对旧版 Microsoft LAPS 的支持，允许将本地管理员账户密码备份到 **Windows Server Active Directory**，满足现有环境需求。

**策略设置与灵活性**

针对每种场景，**Windows LAPS** 提供灵活的策略设置，允许管理员根据组织需求配置以下内容：

- 密码的轮换频率
- 密码的存储位置（本地或云）
- 密码加密选项
- 权限管理和访问控制

# 部署

在使用 Windows LAPS 之前，必须更新 Windows Server Active Directory 架构。此操作通过使用Update-LapsADSchema 执行。

```sql
Update-LapsADSchema
```

该命令将询问您是否要扩展 AD 架构，键入“A”以添加所需的所有架构扩展。

向 OU 对象授予 LAPS 权限。运行以下命令，为管理的 OU 授权密码存储权限：

```sql
Set-LapsADComputerSelfPermission -Identity "OU=LAPS-OU,DC=contoso,DC=intra"
```

验证权限，检查 LAPS 对象属性是否正确配置：

```sql
Get-ACL -Path "AD:OU=LAPS-OU,DC=contoso,DC=intra"
```

配置组策略 创建或编辑组策略对象，导航到 计算机配置 > 管理模板 > 系统 > LAPS。

应用组策略

## LAPS运维

### 通过AD工具进行检索

在AD中，打开对应计算机属性 > LAPS > 查看密码

### 使用PowerShell查看密码

```sql
Get-LapsADPassword -Identity ws2025-03 -AsPlainText
```

### LAPS密码重置

可以使用**Reset-LapsPassword**在本地强制立即轮换密码。

---

参考：

1. [什么是 Windows LAPS？](https://learn.microsoft.com/zh-cn/windows-server/identity/laps/laps-overview)
2. [Windows LAPS：本地管理员密码解决方案](https://www.pangshare.com/3505.htm)
