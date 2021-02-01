---
layout: post
title: V2Board 搭建教程
slug: V2Board build tutorial
date: 2020-01-10 20:34
status: publish
author: Moexin
categories: 
  - 教程
tags:
  - V2Board
excerpt: 记一次基于 Laravel 开发的程序 V2Board 部署安装的详细过程。
---

## 环境要求

这里我们推荐使用aaPanel作为环境搭建的入门首选，机器的内存最好是1G，512M是最低要求配置（Swap最小要求1G）。

本文教程是将 **aaPanel** 作为环境进行配置。

## 部署

### 1.配置aaPanel

你需要在 [aaPanel](https://www.aapanel.com) 选择你的系统获得安装方式。这里以 Debian 9作为系统环境进行安装。

```
apt install curl -y && wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && bash install.sh
```

安装完成后我们登陆 aaPanel 进行环境的安装。

选择使用LNMP的环境安装方式勾选如下信息。

#### 最低要求：

☑️ Nginx 1.17  
☑️ MySQL 5.6  
☑️ PHP 7.3  
☑️ Redis 5.0

#### 个人推荐：

☑️ Nginx Tengine  
☑️ MySQL AliSQL  
☑️ PHP 7.3  
☑️ Redis 5.0

以上环境版本号请选择 Compiled 进行编译安装。

### 2.安装PHP组件

aaPanel 面板 > App Store > 找到PHP 7.3点击Setting > Install extentions
安装以下组件：

☑️ fileinfo  
☑️ opcache  
☑️ redis   
☑️ imagemagick  
☑️ imap  
☑️ exif  
☑️ intl

### 3.解除被禁止的函数

aaPanel 面板 > App Store > 找到PHP 7.3点击Setting > Disabled functions 将 `putenv` `proc_open` `pcntl_alarm` `pcntl_signal`从列表中删除。

### 4.添加站点

aaPanel 面板 > Website > Add site。

```
Domain：填入你指向服务器的域名
Database：MySQL utf8mb4
PHP version：PHP-73
```

Submit 完成创建。

完成创建后访问站点目录删除目录下除`.htaccess`和`.user.ini`以外的所有文件。



### 5.安装V2Board

通过SSH登录到服务器后访问站点路径如：/www/wwwroot/domain.com。

以下命令都需要在站点目录进行执行。

执行命令从 Github 克隆到当前目录。

```
# 默认拉取 V2Board master 分支
git clone -b master https://github.com/v2board/v2board.git tmp && mv tmp/.git . && rm -rf tmp && git reset --hard
```

执行命令更新 composer 程序。

```
composer self-update
```

执行命令进行包安装。

```
composer install
```

安装过程中报错或者无法继续安装的请分配 Swap，如何分配 Swap 请查阅[post]4[/post]

复制.env.example文件为.env。

```
# domain.com 请更改为站点域名且路径必须存在
cp .env.example .env
```

打开 .env 文件，修改数据库信息并保存。

```
DB_HOST=数据库地址
DB_PORT=3306
DB_DATABASE=数据库名
DB_USERNAME=数据库用户名
DB_PASSWORD=数据库密码
```

每次修改 `.env` 文件后需要执行以下命令重建缓存

```
php artisan config:cache
```

保存后请重新给予目录权限

```
# domain.com 请更改为站点域名且路径必须存在
chown -R www:www *
chmod -R 755 *
```

执行命令进行面板的安装。

```
php artisan v2board:install
```

输入管理员账号密码。

### 6.配置站点

编辑添加的站点 > Site directory > Running directory 选择 /public 保存，并且取消勾选Anti-XSS attack (Base directory limit)(open_basedir)。

编辑添加的站点 > URL rewrite 填入伪静态信息。

```
location /downloads {
}

location / {
    try_files $uri $uri/ /index.php$is_args$query_string;
}

location ~ .*\.(js|css)?$
{
    expires 1h;
    error_log off;
    access_log /dev/null;
}
```

#### 禁止访问网站目录下以.开头的文件（可选,会造成证书签发失败，请签发完毕再添加至 URL rewrite 与以上代码共存。）

```
location ~ /\.
{
    deny all;
}
```

至此一切就绪，可以访问你的面板了。

### 7.配置定时任务

aaPanel 面板 > Cron。

```
# domain.com 请更改为站点域名且路径必须存在
Type of Task：Shell Script
Name of Task：Task Scheduling
Period：N Minutes 1 Minute
Script content：/usr/bin/php /www/wwwroot/domain.com/artisan schedule:run
```

根据上述信息添加每1分钟执行一次的定时任务。

### 7.启动队列服务

队列服务将会应用在邮件发送等场景，请务必保证队列服务在后台运行正常。

你可以使用 nohup 让其在后台运行，但是 nohup 无法保证队列服务不会退出。 使用 nohup 方式你需要在站点目录下执行如下命令：

```
nohup php artisan queue:work --queue=send_email,send_telegram > queue.log 2>&1 &
```

如果你想让队列服务长期保持稳定的在后台运作，你需要使用 Systemd 的 Buff 加持。

#### 添加 Systemd 配置文件

```
#以下代码块请更改为站点域名且路径必须存在domain.com并全部一次性复制粘贴回车
cat << EOF >> /etc/systemd/system/queue.service
[Unit]
Description=Queue Service
After=network.target
Wants=network.target

[Service]
Type=simple
PIDFile=/run/queue.pid
ExecStart=/usr/bin/php /www/wwwroot/domain.com/artisan queue:work --queue=send_email,send_telegram
Restart=on-failure

[Install]
WantedBy=multi-user.target
EOF
```

#### 启动由 Systemd 守护的队列服务

```
#重载 Systemd 配置
systemctl daemon-reload
#设置由 Systemd 守护的队列服务开机自启动
systemctl enable queue.service
#启动由 Systemd 守护的队列服务
systemctl start queue.service
```

至此一切就绪，可以直接投入生产使用了。

## 前后分离部署教程

前后分离后用户访问的是前端页面，后端仅提供api供前端使用。  
将前端html文件托管部署到空间或者服务器，亦或者OSS等支持html的存储服务。  
前端分为用户端和管理端：  
用户端文件更新仓库为：https://github.com/v2board/v2board-user/releases  
管理端文件更新仓库为：https://github.com/v2board/v2board-admin/releases  
配置并将 env.example.js 重命名为 env.js 后即完成部署。访问前端域名即可访问。   
### 特别注意
`env.js` 文件下的 `host: '',` 应为你分离后的根域名的二级域名，并且解析到与你授权域名相同的记录值。例如你的授权域名的记录值为 `1.1.1.1` 你在分离后的根域名 `233.com` 下添加一条二级域名解析为 `api.233.com`记录值填写与你授权域名相同的记录值 `1.1.1.1` 然后分离后的根域名解析记录值填写你将前端html文件托管部署到空间或者服务器的CNAME记录值或IP地址，`env.js` 文件下的 `host: '',`则填写为 `host: 'https://api.233.com',`(如果你没有SSL证书请将 `https` 改为 `http`)。至此你就可以访问分离后的根域名 `233.com` 来登录用户端了。管理端同理。