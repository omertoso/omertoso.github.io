---
title: AppLocker 应用访问控制
published: 2024-12-23
description: ''
image: ''
tags: [AppLocker]
category: Windows Server
draft: false 
lang: ''
---

**AppLocker** 是 Windows 提供的一项应用程序控制功能，用于限制和管理企业环境中哪些应用程序可以在计算机上运行。通过配置 AppLocker，企业可以防止未经授权的软件运行，从而提高 IT 环境的安全性。以下是如何在企业中部署和配置 AppLocker 的步骤：

---

# **1. 前提条件**

在部署 AppLocker 前，需要满足以下条件：

- **操作系统要求**：AppLocker 仅适用于 Windows 7 企业版、Windows 8 企业版、Windows 10 企业版以及 Windows Server 2008 R2 和更高版本的操作系统。

- **管理员权限**：需要在 Windows Server 上使用 Group Policy（组策略）进行配置，因此需要管理员权限。

- **Active Directory 环境**：AppLocker 配置通常依赖于 Active Directory (AD) 中的组策略进行管理。



# **2. 配置 AppLocker 的基本步骤**



## **步骤 1：启用 AppLocker 策略**

AppLocker 策略是通过组策略（Group Policy）进行管理的。按照以下步骤启用：

1. **打开组策略管理控制台**：

- 在 Windows Server 中，打开 **Group Policy Management Console (GPMC)**。

- 右键点击域或组织单位 (OU)，然后选择 **Create a GPO in this domain, and Link it here**，创建一个新的 GPO（组策略对象）。

2. **启用 AppLocker 策略**：

- 打开 **Group Policy Management Editor**。

- 导航到 **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Application Control Policies** > **AppLocker**。

- 右键点击 **AppLocker**，然后选择 **Properties**。

- 在 **Properties** 对话框中，启用 **Configured** 并选择所需的策略。



## **步骤 2：配置 AppLocker 策则**

AppLocker 允许管理员配置以下几种类型的规则：

- **可执行文件规则**：控制哪些 EXE 和 MSI 文件可以运行。

- **脚本规则**：控制 PowerShell 脚本、批处理文件（.bat、.cmd）等脚本的执行。

- **Windows Installer 规则**：控制 MSI 文件的安装。

- **包规则**：控制 UWP（Universal Windows Platform）应用程序的安装和执行。



1. 在 AppLocker 策略的 **Application Control Policies** 下，选择需要配置的规则类型（例如 **Executable Rules**）。
2. 右键点击相应规则类型，选择 **Create New Rule** 创建新规则。
3. 根据需求配置规则：

- **允许/拒绝规则**：创建规则来允许或拒绝特定的应用程序执行。

- **条件选择**：可以根据文件的发布者、路径、哈希值等属性来定义规则。

- **设置规则执行**：确保将规则应用到正确的用户组或计算机。



## **步骤 3：测试和验证规则**

- **测试规则**：在生产环境部署之前，建议先在测试环境中验证 AppLocker 配置。可以通过 **Audit Mode**（审核模式）启用规则，这样不会直接阻止程序的执行，而是记录日志，帮助你查看哪些应用程序会被阻止。

- 审核模式下，AppLocker 会记录每个被阻止应用程序的执行事件，但不会实际拦截程序运行。

- **验证配置**：测试配置是否按预期工作，检查日志文件中的事件，确认是否正确阻止了未经授权的程序。



## **步骤 4：启用强制执行模式**

一旦测试完成并验证规则无误，可以将 **Audit Mode** 更改为 **Enforce Mode**，这将实际阻止不符合规则的应用程序运行。

- 在 AppLocker 配置中，将所有规则切换到 **Enforce** 模式，以开始强制执行这些策略。



## **步骤 5：维护和更新规则**

- **定期审核**：定期检查和审核 AppLocker 策略，确保它们始终符合组织的安全要求。

- **更新规则**：如果有新的应用程序需要使用，或者需要更新现有应用程序的规则，可以通过 **AppLocker Console** 或组策略管理来修改现有规则。



# **3. 集中管理与分配**

通过 **组策略管理** 可以集中管理 AppLocker 策略，将其应用到整个组织或特定的计算机组：

- **分配到计算机组**：你可以将 AppLocker 策略应用到特定的计算机组或 OU（组织单位），以控制哪些计算机上执行哪些程序。

- **使用安全组**：根据用户组或设备组来分配不同的规则。例如，开发人员和普通用户可能需要不同的应用程序访问权限。



# **4. 常见的 AppLocker 使用场景**

1. **限制运行未经授权的应用程序**：企业可以使用 AppLocker 来确保只有经过批准的应用程序能够在公司设备上运行，从而防止恶意软件或未经授权的软件在设备上执行。
2. **确保合规性**：在某些行业或环境中（如金融、医疗、政府等），AppLocker 可以帮助企业符合严格的合规性要求，限制不安全的程序。
3. **减少恶意软件传播**：通过阻止未经授权的程序，AppLocker 可有效减少恶意软件通过软件漏洞传播的风险。
4. **控制软件安装**：管理哪些用户或设备可以安装和运行特定类型的应用程序，提升对软件环境的控制。

---

参考：

1. [Microsoft AppLocker](https://learn.microsoft.com/zh-cn/windows/security/application-security/application-control/app-control-for-business/applocker/applocker-overview)
