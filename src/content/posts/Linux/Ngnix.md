---
title: Ngnix
published: 2024-12-23
description: ''
image: ''
tags: ['Ngnix']
category: 'Linux'
draft: false 
lang: ''
---

### Nginx 基础概念

首先，需要理解 Nginx 的基本功能和使用场景。Nginx 主要有以下几个用途：

- Web 服务器：处理 HTTP 请求，静态文件和动态内容的处理。
- 反向代理：将客户端请求转发给后端服务器进行处理，隐藏后端服务器的详细信息。
- 负载均衡：通过多台服务器分担请求负载，提高网站的处理能力和可靠性。
- 内容缓存：缓存动态内容，提高系统性能。

理论上，Nginx支持的并发连接上线取决于内存。

#### 进程

在 **Nginx** 中，worker 进程 和 master 进程 是其核心架构的一部分，基于 **多进程模型**，实现高性能和高并发的请求处理。

master ：在Nginx启动后，由操作系统创建，管理 worker 进程不处理任何客户端请求，负责整体进程管理和与系统交互。

worker：每个 worker 进程是由 master 进程派生的，通过worker_processes 参数设置，通常设置为服务器 CPU 核心数，一个 worker 进程崩溃不会影响其他 worker 进程

:::note
Mac
:::

brew install nginx
sudo nginx
brew services star nginx

:::note
Centos 看到 centos 的欢迎界面即可，不同系统 Nginx 的 Welcome 不一样
:::

sudo yum install epel-release
sudo yum install nginx
sudo systemctl start nginx
sudo systemctl status nginx

安装
```shell
sudo yum install -y gcc # C 编译工具
sudo yum install -y pcre pcre-devel # 识别正择表达式
sudo yum install -y zlib zlib-devel # gzip 格式压缩
sudo yum install -y openssl openssl-devel # SSL 支持
```

#### Linux 内核参数优化

修改 /ect/sysctl.conf 文件，执行 sysctl -p 命令生效

在前台运行
nginx -g "daemon off;"



# 多台服务器同时运行 Nginx 的场景

在企业环境中，是否需要多台服务器同时运行 Nginx 取决于您的业务需求、流量规模、可用性要求以及架构设计。以下几种场景可能需要在多台服务器上同时运行 Nginx：

## 1. 高可用性和负载均衡

如果您的网站或应用需要高可用性（HA）并能够承受大量的流量，您可能需要在多台服务器上部署多个 Nginx 实例。这通常涉及到以下几个方面：

- **负载均衡**：当流量增长时，将负载分散到多台服务器上，避免单台服务器成为瓶颈。多个 Nginx 实例（负载均衡器）可以将请求分配到后端服务器（如应用服务器或数据库服务器）。
  
- **高可用性**：通过部署多个 Nginx 实例，您可以确保一个 Nginx 实例故障时，其他实例可以继续服务，保证系统的连续性。

在这种架构中，通常有一个负载均衡器来均衡流量，并将请求分发到不同的 Nginx 实例上。

### 示例：

假设您的 Web 应用部署在三台应用服务器上，您可以在另一台 Nginx 服务器上配置负载均衡，将请求分发到这三台应用服务器。

```nginx
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}

server {
    listen 80;
    location / {
        proxy_pass http://backend;
    }
}
```



随着学习的深入，可以学习更多高级功能：

- 负载均衡算法：如 round-robin、least_conn、ip_hash 等。
- 动态模块：例如，ngx_http_rewrite_module 用于重写 URL，ngx_http_ssl_module 用于启用 SSL。
- 限流与防火墙：配置访问控制、限制请求频率、阻止恶意访问。

---

参考：

1. [官方文档](https://nginx.org/en/docs/)

2. [W3Cschool Nginx文档](https://www.w3cschool.cn/nginxsysc/)

3. [《深入理解Nginx》](https://www.alipan.com/s/M6t4yjwQhYH)
