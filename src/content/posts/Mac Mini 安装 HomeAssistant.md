---
title: Mac Mini 安装 HomeAssistant
published: 2024-12-28
description: ''
image: ''
tags: ['智能家居']
category: ''
draft: false 
lang: ''
---

# 前言

小米最近给 HA 提供了官方插件，正好手里有小米智能家居来部署下，查看官方文档本地部署比较方便。

**需要的环境**

1. brew 如无运行安装
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. python
   ```bash
   brew install python@3.10
   ```

# 配置

创建 python 虚拟环境

```shell
mkdir ~/Documents/HomeAssistant
cd ~/Documents/HomeAssistant
python3 -m venv .
source bin/activate
```

安装 whell
```shell
python3 -m pip install --upgrade pip
python3 -m pip install wheel
```

安装 homeassistant
```shell
pip3 install homeassistant==2023.1.7
```

后台运行 hass
```shell
nohup hass &
```

## error

- 端口被占用
  检查端口占用情况、杀死占用端口的进程、重新启动 Home Assistant

  ```bash
  lsof -i :8123
  
  kill -9 <占用端口的进程ID>
  
  nohup hass &
  ```

  
