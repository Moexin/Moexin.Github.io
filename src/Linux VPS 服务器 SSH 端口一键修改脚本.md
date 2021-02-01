---
layout: post
title: Linux VPS 服务器 SSH 端口一键修改脚本
slug: Linux VPS server SSH port one-click modification script
date: 2020-04-10 20:34
status: publish
author: Moexin
categories: 
  - 脚本
tags:
  - Linux
  - Shell
  - 一键脚本
  - SSH
excerpt: 我们的很多 VPS 服务器，默认的端口都是 22，所以一直会被人扫描爆破，很容易会出现问题，所以我们需要通过修改端口来尽可能减少这种事情发生，但对于很多小白或者很懒的人来说，更喜欢一键脚本就能完成的方法，于是我就整了个 SSH 端口一键修改脚本。从 OneinStack 一键安装包上扒下来的。
---

> 我们的很多`VPS`服务器，默认的端口都是`22`，所以一直会被人扫描爆破，很容易会出现问题，所以我们需要通过修改端口来尽可能减少这种事情发生，但对于很多小白或者很懒的人来说，更喜欢一键脚本就能完成的方法，于是我就整了个`SSH`端口一键修改脚本。从`OneinStack`一键安装包上扒下来的。

## 使用方法

**系统要求：**支持`Debian`、`Ubuntu`、`CentOS`系统。

运行以下命令：

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/SSH-Port.sh)
```

输入端口确认。再打开防火墙端口：

```
#如果防火墙使用的iptables（Centos 6），修改端口为8080
iptables -I INPUT -p tcp --dport 8080 -j ACCEPT
service iptables save
service iptables restart
#如果使用的是firewall（CentOS 7）
firewall-cmd --zone=public --add-port=8080/tcp --permanent 
firewall-cmd --reload
```

最后重启`SSH`生效：

```
#CentOS系统
service sshd restart
#Debian/Ubuntu系统
service ssh restart
```

然后就可以使用新端口SSH登录了。