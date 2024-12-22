---
title: PowerShell 常用命令
published: 2024-12-22
description: ''
image: ''
tags: [PowerShell]
category: Windows Server
draft: false 

---

| **功能分类**       | **命令**                  | **用途**                     | **示例**                                                     |
| ------------------ | ------------------------- | ---------------------------- | ------------------------------------------------------------ |
| **系统信息查看**   | `Get-Process`             | 查看当前运行的进程           | `Get-Process`                                                |
|                    | `Get-Service`             | 列出所有服务及其状态         | `Get-Service`                                                |
|                    | `Get-EventLog`            | 查看系统事件日志             | `Get-EventLog -LogName System`                               |
|                    | `Get-ComputerInfo`        | 获取计算机详细信息           | `Get-ComputerInfo`                                           |
|                    | `Get-WmiObject`           | 通过 WMI 获取系统信息        | `Get-WmiObject Win32_OperatingSystem`                        |
| **文件与目录管理** | `Get-ChildItem` (或 `ls`) | 列出文件和文件夹             | `Get-ChildItem C:\Windows`                                   |
|                    | `New-Item`                | 创建文件或文件夹             | `New-Item -Path C:\Test -ItemType Directory`                 |
|                    | `Remove-Item`             | 删除文件或目录               | `Remove-Item C:\Test -Recurse`                               |
|                    | `Copy-Item`               | 复制文件或目录               | `Copy-Item C:\Test\File.txt C:\Backup`                       |
|                    | `Move-Item`               | 移动或重命名文件/文件夹      | `Move-Item C:\Test\File.txt D:\`                             |
| **网络管理**       | `Test-Connection`         | 测试网络连接（类似 ping）    | `Test-Connection www.google.com`                             |
|                    | `Get-NetIPAddress`        | 查看本机 IP 地址             | `Get-NetIPAddress`                                           |
|                    | `New-NetIPAddress`        | 手动分配 IP 地址             | `New-NetIPAddress -InterfaceAlias Ethernet0 -IPAddress 192.168.1.100 -PrefixLength 24` |
|                    | `Get-NetAdapter`          | 查看网络适配器信息           | `Get-NetAdapter`                                             |
| **权限与用户管理** | `Get-LocalUser`           | 查看本地用户                 | `Get-LocalUser`                                              |
|                    | `New-LocalUser`           | 创建本地用户                 | `New-LocalUser -Name TestUser -Password (ConvertTo-SecureString "Password123" -AsPlainText -Force)` |
|                    | `Remove-LocalUser`        | 删除本地用户                 | `Remove-LocalUser -Name TestUser`                            |
|                    | `Get-LocalGroup`          | 查看本地用户组               | `Get-LocalGroup`                                             |
|                    | `Add-LocalGroupMember`    | 将用户添加到组               | `Add-LocalGroupMember -Group Administrators -Member TestUser` |
| **任务与服务管理** | `Start-Service`           | 启动服务                     | `Start-Service -Name wuauserv`                               |
|                    | `Stop-Service`            | 停止服务                     | `Stop-Service -Name wuauserv`                                |
|                    | `Restart-Service`         | 重启服务                     | `Restart-Service -Name wuauserv`                             |
|                    | `Get-ScheduledTask`       | 查看计划任务                 | `Get-ScheduledTask`                                          |
|                    | `New-ScheduledTask`       | 创建计划任务                 | `New-ScheduledTask -Action (New-ScheduledTaskAction -Execute "notepad.exe")` |
| **系统配置**       | `Set-Date`                | 设置系统时间                 | `Set-Date -Date "2024-12-31 12:00:00"`                       |
|                    | `Get-TimeZone`            | 获取当前时区                 | `Get-TimeZone`                                               |
|                    | `Set-TimeZone`            | 修改系统时区                 | `Set-TimeZone -Name "China Standard Time"`                   |
| **脚本与自动化**   | `Invoke-Command`          | 在本地或远程计算机上执行命令 | `Invoke-Command -ScriptBlock { Get-Process }`                |
|                    | `Start-Job`               | 后台运行任务                 | `Start-Job -ScriptBlock { Get-Process }`                     |
|                    | `Get-Job`                 | 查看正在运行的任务           | `Get-Job`                                                    |
|                    | `Stop-Job`                | 停止后台任务                 | `Stop-Job -Id 1`                                             |
