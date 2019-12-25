---
layout:     post
title:      配置ubuntu系统一些你用得上的内容
subtitle:   配置新的服务器
date:       2019-12-25
author:     Johnny
header-img: img/post_bao_yan.jpg
catalog: true
tags:
    - 杂
---

## 配置静态ipv6地址
首先进入编辑界面
```
vi /etc/network/interfaces
```

再添加
```
iface eth0 inet6 static
```

## 配置新用户

这里推荐这种方式

```
useradd -d /home/user_name -m user_name
```
在home/下创建一个user_name 目录

之后再配置密码

```
passwd user_name
```

为该用户指定命令解释程序（通常为/bin/bash）
···
usermod -s /bin/bash user_name
···

删除账号
```
userdel -r user_name
```
-r 参数为删除该目录下所有的文件
