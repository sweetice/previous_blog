---
layout:     post
title:      How to install cuda on ubuntu 1804
subtitle:   Enjoy Deep learning
date:       2019-02-20
author:     Johnny
header-img: img/post_bao_yan.jpg
catalog: true
tags:
    - 杂
---

# 在ubuntu1804上安装cuda

- 1.查看是否支持CUDA，清理掉原来的驱动

使用如下命令：
```
lspci | grep -i nvidia
```

我得到的输出是：

```
01:00.0 VGA compatible controller: NVIDIA Corporation GP104 [GeForce GTX 1070 Ti] (rev a1)
01:00.1 Audio device: NVIDIA Corporation GP104 High Definition Audio Controller (rev a1)
```

说明我的显卡是1070Ti。

再清理掉原来的驱动

```
sudo apt-get autoremove --purge nvidia*
```

- 2.禁用nouveau
在终端运行

```
$ lsmod | grep nouveau
```

如果有输出，说明nouveau正在运行，需要手动禁掉nouveau。

使用

```
$ sudo vim /etc/modprobe.d/blacklist-nouveau.conf
```

在文件内写入：

```
blacklist nouveau 
options nouveau modeset=0
```

执行

```
$ sudo update-initramfs -u
```

确定是否禁用成功

```
$ lsmod | grep nouveau
```

- 3.安装驱动

此处建议使用ubuntu自带的software & updates安装驱动。
- 1) 打开Software & Updates
- 2) 点击Additional Drivers
- 3) 选用 Using NVIDIA driver metapackage from nvidia-diver-390(proprietary, tested)

![Software and Updates](https://github.com/sweetice/sweetice.github.io/blob/master/figures/software%20and%20updates.png)




