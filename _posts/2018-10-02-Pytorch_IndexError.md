---
layout:     post
title:      Pytorch IndexError
subtitle:   索引错误，太多索引
date:       2018-10-04
author:     Johhny
header-img: img/bg-pytorch.jpg
catalog: true
tags:
    - Pytorch
    - Debug
---


# Pytorch 4.0 报错 IndexError: too many indices for array

出现问题的原因：pytorch 3.0 和 4.0以上版本不兼容，数据无法自动转换格式

```
action = action.data.numpy()[0].astype('int32')
```

改为
```
action = action.data.numpy()[0].astype('int32')
```

就可以了
