---
layout: post
title: Linux VPS 一键添加/删除 Swap 虚拟内存脚本
slug: Linux VPS one-click add/remove Swap virtual memory script
date: 2020-03-10 20:34
status: publish
author: Moexin
categories: 
  - 脚本
tags:
  - Linux
  - Shell
  - 一键脚本
  - Swap
  - 虚拟内存
excerpt: 很多人的VPS服务器由于内存太小，会导致很多进程被杀掉，这时候就需要我们添加 Swap 虚拟内存了，这里就整了个一键脚本方便懒人或小白使用。
---

> 很多人的VPS服务器由于内存太小，会导致很多进程被杀掉，这时候就需要我们添加`Swap`虚拟内存了，这里就整了个一键脚本方便懒人或小白使用。

## 使用方法

**注意：** 脚本不支持`OpenVZ`架构，安装会自动退出。

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/Swap.sh)
```
然后根据选项进行操作，记得添加`Swap`的时候填写纯数字，默认单位为M。

![运行截图](https://cdn.jsdelivr.net/gh/MoexinCDN/Picture@master/20191217151814.png)