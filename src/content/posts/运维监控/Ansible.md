---
title: Ansible
published: 2024-12-25
description: ''
image: ''
tags: ['Ansible']
category: '运维监控'
draft: false 
lang: ''
---

# 前言

Ansible默认通过 SSH 协议管理机器，**配置管理**、**应用部署**和**任务自动化**。

- **Agentless:** Ansible 不需要在目标主机上安装代理，只需通过 SSH 连接。

- **Playbooks:** 使用 YAML 编写的自动化脚本，用于定义任务。

- **Inventory:** 定义目标主机列表，可以是静态文件或动态生成。

- **Modules:** 预定义的任务模块，用于完成具体操作（如文件管理、服务启动等）。

- **Roles:** 用于组织和复用配置，方便管理复杂项目。

- **Ad-hoc Commands:** 用于执行简单的单次命令。

```bash
# inventory 默认目录
/opt/homebrew/Cellar/ansible/11.1.0_1/inventory
# 配置好IP后，分发ssh密钥
# 在 Ansible 主机上运行 （前提已配好ssh）
ssh-copy-id 目标主机名次@目标主机IP  
# 使用 Ad-hoc 命令测试连接：
ansible all -i inventory -m ping
```

## 监控

可以通过写 Playbooks 方式收集主机信息，使用脚本将日志连入Prometheus。

Prometheus 配置

```bash
scrape_configs:
  - job_name: 'ansible'
    static_configs:
      - targets: ['<exporter_ip>:9100']
```

# 安全问题

于控制主机（Ansible 控制节点）通过 SSH 管理所有目标主机（Inventory 中的主机），一旦控制主机被攻破，黑客可能会获取对所有目标主机的控制权限。因此，需要采取以下安全措施来降低风险：

1. **最小化权限**：控制用户权限，防止过多访问。
2.	**数据加密**：使用 Vault 加密敏感数据。
3.	**隔离环境**：控制节点与公网隔离，必要时使用跳板机。
4.	**监控和审计**：记录所有操作并实时监控异常活动。



---

参考：

1. [Ansible中文权威指南](https://ansible-tran.readthedocs.io/en/latest/)
