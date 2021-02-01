---
layout: post
title: Linux 一键安装常见/最新内核脚本 锐速/BBR/BBR魔改版/BBRPlus/BBR2
slug: Linux one-click installation of common/latest kernel scripts Rui Su/BBR/BBR magic revision/BBRPlus/BBR2
date: 2020-07-10 20:34
status: publish
author: Moexin
categories: 
  - 脚本
tags:
  - Linux
  - Shell
  - 一键脚本
  - 网络加速
excerpt: 对于出口带宽，我们常常采用BBR，锐速等TCP加速软件来争夺带宽提高自己的速度。但是原版的BBR并没有太多侵略性，在这个人人都用TCP加速的大环境下，BBR的加速功效就略显不足了。于是大佬们专门改进了下这个BBR，使BBR具有了侵略性。最近我也连续购买了几个服务器，每次都手动搭建，感觉到十分麻烦，干脆给大家推荐一个脚本吧。该脚本支持的加速软件非常多，支持锐速、BBR、BBR魔改版、BBRPlus、BBR2等。
---

> 对于出口带宽，我们常常采用`BBR`，`锐速`等`TCP`加速软件来争夺带宽提高自己的速度。但是原版的`BBR`并没有太多侵略性，在这个人人都用`TCP`加速的大环境下，`BBR`的加速功效就略显不足了。于是大佬们专门改进了下这个`BBR`，使`BBR`具有了侵略性。最近我也连续购买了几个服务器，每次都手动搭建，感觉到十分麻烦，干脆给大家推荐一个脚本吧。该脚本支持的加速软件非常多，支持`锐速`、`BBR`、`BBR魔改版`、`BBRPlus`、`BBR2`等。

## 用法

```
wget --no-check-certificate -q https://cdn.jsdelivr.net/gh/ylx2016/Linux-NetSpeed@master/tcp.sh && chmod +x tcp.sh && ./tcp.sh
```

**注意：**此脚本会安装您所选择的内核并卸载其他原内核，具有一定风险性，安装中会出现提示`Abort kernel removal?`选择`No`即可。如果不想卸载原内核，请使用以下不卸载内核版本。

```
wget --no-check-certificate -q https://cdn.jsdelivr.net/gh/ylx2016/Linux-NetSpeed@master/tcpx.sh && chmod +x tcpx.sh && ./tcpx.sh
```

然后根据提示按需操作即可。

![脚本截图][1]


  [1]: https://cdn.jsdelivr.net/gh/MoexinCDN/Picture@master/20200823232951.png