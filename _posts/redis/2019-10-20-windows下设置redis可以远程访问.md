---
layout: post
title: redis在windows下设置远程访问
categories: redis
description: redis在windows下设置远程访问
keywords: redis, 远程访问
---

近日在做项目开发demo时，发现安装在windows下的redis无法设置远程连接，就算在本地也无法通过绑定的ip地址进行访问。

win7 环境 192.168.25.20

通过 192.168.25.20 访问报错，说是redis处于保护模式下，无法通过ip进行访问，只能是内部循环访问。查了一下资料

说是要注释 #127.0.0.1 将protected-mode-yes 改为 protected-no 即可，但是还是不起作用

几经思考，发现我的启动方式就是直接启动的redis-server服务。没有指定启动的配置文件。

再查资料的时候，发现redis的启动方式应该如下

1，在redis安装目录下，将redis安装进服务管理

redis-server --service-install redis.windows.conf --loglevel verbose

2, 开启redis服务即可

redis-server --service-start

这样就可以进行远程访问了

3，其他命令

- 停止服务 ： redis-server --service-stop


- 卸载服务 redis-server --service-uninstall