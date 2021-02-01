---
layout: post
title: Debian/Ubuntu/CentOS 全自动网络重装一键脚本
slug: Debian/Ubuntu/CentOS automatic network reinstallation one-click script
date: 2020-02-10 20:34
status: publish
author: Moexin
categories: 
  - 脚本
tags:
  - Linux
  - Shell
  - 一键脚本
  - 重装系统
excerpt: 本一键脚本在萌咖大佬的脚本基础上开发，实现了懒人式一键网络重装 Debian / Ubuntu / CentOS 系统及DD方式安装系统。解决了云服务商提供模板镜像体积过大、预装软件过多、不够纯净等问题。
---

>本一键脚本在萌咖大佬的脚本基础上开发，实现了懒人式一键网络重装 Debian / Ubuntu / CentOS 系统及DD方式安装系统。解决了云服务商提供模板镜像体积过大、预装软件过多、不够纯净等问题。

# 使用方法

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/hiCasper/Shell@master/AutoReinstall.sh)
```

# 支持重装的系统

*   Ubuntu 18.04/16.04
*   Debian 9/10
*   CentOS 6
*   CentOS 7 （DD方式）
*   自定义DD镜像

# 特性 / 优化

*   自动获取IP地址、网关、子网掩码
*   自动判断网络环境，选择国内/外镜像，解决速度慢的问题
*   懒人一键化，无需复杂的命令
*   解决萌咖脚本中一些导致安装错误的问题
*   CentOS 7 镜像抛弃LVM，回归ext4，减少不稳定因素

# 注意

*   重装后系统密码均在脚本中有提供，**安装后请尽快修改密码**，Linux系统建议启用密钥登陆。
*   OpenVZ / LXC 架构系统不适用