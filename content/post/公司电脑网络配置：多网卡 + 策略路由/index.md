---
title: "工作电脑网络配置：多网卡 + 策略路由"
summary: "我在公司必须通过连接网线的方式上网：配置有线网卡的IP地址11.2.9.11、子网掩码255.255.255.192、网关11.2.9.1; DNS1: 10.33.176.12, DNS2: 10.33.176.13），同时还需要配置HTTPS代理为10.22.98.22后才能访问外网。本文主要介绍当需要访问10.*或11.*等内网时，使用有线网络；当访问外网时就通过连接Wi-Fi网络的方法。"

date: 2026-02-12T21:34:32+08:00
lastmod: 2026-02-12T21:34:32+08:00

categories:
 - 经验积累
tags:
  - 网络
  - IP地址
  - 路由
  - 网关
  - 代理
  - MacOS
  - Windows


# Post's origin author name
#author:
# Post's origin link URL
#link:
# Image source link that will use in open graph and twitter card
#imgs:
# Expand content on the home page
#expand: true
# It's means that will redirecting to external links
#extlink:
# Disabled comment plugins in this post
#comment:
# enable: false
# Disable table of content int this post
# Notice: By default will automatic build table of content 
# with h2-h4 title in post and without other settings
#toc: false
# Absolute link for visit
#url: "工作电脑网络配置：多网卡 + 策略路由.html"
# Sticky post set-top in home page and the smaller number will more forward.
#weight: 1
# Support Math Formulas render, options: mathjax, katex
#math: mathjax
---

这是一个**典型的多网卡 + 策略路由（Policy Routing）场景**，目标是：

- 访问 `10.*`、`11.*` 走有线网卡（不用配代理）
- 其它流量走WiFi（WiFi 作为默认出口）

<br>

## 原始方案

```
						┌────────────┐
            │   PC/MAC   │
            └─────┬──────┘
                  │
              	有线网卡
           (默认网关11.2.9.1) 
                  │
             Proxifier策略
             			│
        ┌─────────┴─────────┐
        │                   │
     外网域名            10.* 或 11.*
     		│									(直连内网) 
    HTTPS Proxy
  (10.22.98.22)               
        │               
     Internet
```

<br>

## 解决方案

```
            ┌────────────┐
            │   PC/MAC   │
            └─────┬──────┘
                  │
        ┌─────────┴─────────┐
        │                   │
     WiFi网卡             有线网卡
  (默认路由出口)        (内网专用路由)
        │                   │
    Internet         		10.* 或 11.*
    (直连外网)            (直连内网)       
```

<br>

### 原理

- **默认路由（default gateway）只能有一个**，否则冲突。
- **移除有线连接的默认网关**（即不让有线网络接管所有流量），只保留其子网路由。
- **手动添加特定目的网段的路由（10.0.0.0/8 和 11.0.0.0/8）指向有线网关（11.2.9.1）**。
- Wi-Fi 接口将作为默认出口（保留其默认网关）。
- 不再需要配置HTTPS 代理（10.22.98.22），旧方案中也是通过Proxifier设置的代理分流规则（10.*和11.*都用直连，其它情况，即访问外网时才需要通过代理）

<br>

### MacOS

1. **同时连接 WiFi + 网线**

   - WiFi 连接外部网络
   - 网线插上公司网络（静态 IP 配置）

   

2. **设置网络优先级**

   打开系统设置 → 网络 → 右上角 `⋯` → 设置服务顺序

   拖动顺序为：

   - **WiFi（最上）**
   - 有线网卡（USB Ethernet / Ethernet）

   

3. **添加静态路由**

   打开终端，执行：

   ```bash
   # 10.0.0.0/8 走有线网关
   sudo route -n add -net 10.0.0.0/8 11.2.9.1
   
   # 11.0.0.0/8 走有线网关
   sudo route -n add -net 11.0.0.0/8 11.2.9.1
   ```

   

4. **验证路由是否生效**

   ```bash
   netstat -rn | grep -E "10\.|11\."
   
   # 应该看到类似输出
   10/8        11.2.9.1
   11/8        11.2.9.1
   default     192.168.66.1   # WiFi网关
   ```

<br>

### Windows

1. **配置有线网络（不要设默认网关）**

   - 打开“网络和共享中心” → 更改适配器设置
   - 右键“以太网” → 属性 → Internet 协议版本 4 (TCP/IPv4) → 属性
   - 手动设置：
     - IP 地址：`11.2.9.11`
     - 子网掩码：`255.255.255.192`
     - **网关：留空（关键！❗ 如果填了网关，Windows 会自动添加默认路由（0.0.0.0/0），导致所有流量走有线，破坏你的策略。）**
     - DNS：`10.33.176.12`、`10.33.176.13`

   

   2. 配置 Wi-Fi（正常自动获取或设网关，作为默认出口）

      

   3. 添加策略路由（以管理员身份运行 CMD 或 PowerShell）

       ```cmd
       route add 10.0.0.0 mask 255.0.0.0 11.2.9.1 metric 10 if <有线接口索引>
       route add 11.0.0.0 mask 255.0.0.0 11.2.9.1 metric 10 if <有线接口索引>
       ```

       > 🔍 如何查接口索引？
       >
       > ```cmd
       > route print  #或用route print 4（强制Ipv4）
       > ```
       >
       > 找到“接口列表”中以太网对应的数字（比如 15）
       
       
       
       
       ```cmd
       # 示例（假设以太网接口索引是 15）：
       route add 10.0.0.0 mask 255.0.0.0 11.2.9.1 if 15
       route add 11.0.0.0 mask 255.0.0.0 11.2.9.1 if 15
       ```
   
   
   
   4. （可选）让路由永久生效
   
       临时路由重启后会消失。要永久添加：
   
       ```cmd
       # （`-p` 表示 persistent）
       route -p add 10.0.0.0 mask 255.0.0.0 11.2.9.1 if 15
       route -p add 11.0.0.0 mask 255.0.0.0 11.2.9.1 if 15
       ```
   
      

