---
layout: post
title: Linux 软件源一键更换脚本
slug: Linux software source one-click replacement script
date: 2020-06-10 20:34
status: publish
author: Moexin
categories: 
  - 脚本
tags:
  - Linux
  - Shell
  - 一键脚本
  - 软件源
excerpt: 有时候会遇到 Linux 的源更新速度非常的缓慢，特别是在国内使用默认的源，因为国内的网络环境，经常会出现无法更新，更新缓慢的情况。在这种情况下，更换一个更适合或者说更近，更快的软件源，会为你的 Linux 安装更新操作更加的流畅和顺利。
---

> 有时候会遇到`Linux`的源更新速度非常的缓慢，特别是在国内使用默认的源，因为国内的网络环境，经常会出现无法更新，更新缓慢的情况。在这种情况下，更换一个更适合或者说更近，更快的软件源，会为你的`Linux`安装更新操作更加的流畅和顺利。

本脚本适合`CentOS 5、6、7`，`Ubuntu 14.04、16.04、18.04`，`Debian 7、8、9`，一键匹配换源。

手动更换源也非常的简单，只需要按几步即可完成，这个脚本只是把这简单的几步用一键完成，为你更换更快的软件源。虽然比较简单，但对管理多台`Linux`服务器的人，或是经常重装系统的人来说能方便不少。

废话不多说，脚本纯净，除了修改软件源文件，不会另外添加其他任何文件或配置，也不会修改其他无关的设置，无残留，代码不加密，这也是我的脚本的原则，功能代码只有一百来行，请自查。

## 用法

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/Mirror.sh)
```

对于 Debian 默认换源为`Fastly CDN`的`Mirror`这个源有`Fastly`的加持对境外主机都有不错的速度。 对于`Ubuntu`和`CentOS`系统都默认换为`阿里云`的`Mirror`这个源有`阿里云全球CDN`的加持，全球都有不错的速度。

对于`Debian`系统还设置了四套其他的源，`阿里云`，`CloudFront CDN`，`网易163`，`中科大的源`，请根据需要使用参数一键设置如

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/Mirror.sh) cn
```

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/Mirror.sh) 163
```

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/Mirror.sh) aliyun
```

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/Mirror.sh) aws
```

如果对配置的文件不满意，还可以一键还原

```
bash <(wget --no-check-certificate -qO- https://cdn.jsdelivr.net/gh/Moexin/Shell@master/Mirror.sh) restore
```

源码查看:
[https://raw.githubusercontent.com/Moexin/Shell/master/Mirror.sh][1]


  [1]: https://raw.githubusercontent.com/Moexin/Shell/master/Mirror.sh