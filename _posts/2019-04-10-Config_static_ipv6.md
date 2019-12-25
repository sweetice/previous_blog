---
layout:     post
title:      设置静态IPV6地址
subtitle:   在ubuntu系统中
date:       2019-04-11
author:     Johnny
header-img: img/post_bao_yan.jpg
catalog: true
tags:
    - Reinforcement Learning
---

```
vi /etc/network/interfaces
```

再添加
```
iface eth0 inet6 static
```
