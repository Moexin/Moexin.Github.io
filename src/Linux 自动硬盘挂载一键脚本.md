---
layout: post
title: Linux 自动硬盘挂载一键脚本
slug: Linux automatic hard disk mounting one-click script
date: 2020-05-10 20:34
status: publish
author: Moexin
categories: 
  - 脚本
tags:
  - Linux
  - Shell
  - 一键脚本
  - 硬盘挂载
excerpt: 在购买服务器时 ，磁盘经常只有固定的5-10G，当你购买额外的空间、或是原本有空间需要挂载时，繁琐的程序会让很多萌新崩溃，而且也不一定能成功挂载~一不小心还把数据丢了。这里推荐一个BT上的一键硬盘挂载脚本~ 支持Centos、Ubuntu、Debian、Fedora。
---

> 在购买服务器时 ，磁盘经常只有固定的5-10G，当你购买额外的空间、或是原本有空间需要挂载时，繁琐的程序会让很多萌新崩溃，而且也不一定能成功挂载~一不小心还把数据丢了。这里推荐一个BT上的一键硬盘挂载脚本~ 支持Centos、Ubuntu、Debian、Fedora。

## 说明：

1：本工具默认将数据盘挂载到`/www`目录  
2：如有`NTFS/FAT32`分区可选格式化自动挂载  
3：若您的硬盘已分区，且未挂载，工具会自动将分区挂载到`/www`  
4：若您的硬盘是新硬盘，工具会自动分区并格式化成`xfs/ext4`文件系统  
5：本工具只自动挂载一个分区，若您有多块数据盘，请手动挂载未被自动挂载的硬盘  
6：此脚本只适用于新硬盘挂载，若数据盘已有数据请勿使用此脚本

## 使用：

```
bash <(wget --no-check-certificate -qO- https://download.bt.cn/tools/auto_disk.sh)
```

如需挂载其他目录在挂载命令后加上挂载目录即可 务必以`/`为开头  
以下挂到`/website`目录为例

```
bash <(wget --no-check-certificate -qO- https://download.bt.cn/tools/auto_disk.sh) /website
```