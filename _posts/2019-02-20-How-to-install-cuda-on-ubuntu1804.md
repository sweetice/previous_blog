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

# 深度学习环境的安装 ubuntu 1804

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
- 1 打开Software & Updates
- 2 点击Additional Drivers
- 3 选用 Using NVIDIA driver metapackage from nvidia-diver-390(proprietary, tested)

![Software and Updates](https://github.com/sweetice/sweetice.github.io/blob/master/figures/software%20and%20updates.png)

如果没有成功，那么就去[官网](https://www.nvidia.cn/Download/index.aspx?lang=cn)选择对应的版本安装。

![nvidia-driver](https://github.com/sweetice/sweetice.github.io/blob/master/figures/nvidia-driver.png)

下载好之后，使用alt+ctrl+f1切换到tty1模式去，从ubuntu1804开始，可以不禁用lightdm了。

使用如下的命令安装

```
$ sudo bash ./NVIDIA-Linux-x86_64-410.93.run 

```
安装完成之后，切换回图形界面。
接下来。

- 4.安装cuda

上[官网](https://developer.nvidia.com/cuda-90-download-archive)下载cuda9.0的包。

```
https://developer.nvidia.com/cuda-90-download-archive
```

之后，关闭掉图形界面（方法同上），进入下载目录，执行如下命令：  
```
$ sudo ./cuda_9.0_linux.run --verbose -silent --toolkit --override 
```
**一定要加入后面的参数**  

这样子不用经过繁琐的选择，能够直接安装上cuda。

现在你还缺少了一些库，安装他们

```
$ sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev
```

快要成功了，接下来添加一下环境变量

```
$ cd ~
```

```
$ sudo gedit ./bashrc
```

在文件的最后，加上：

```
export PATH="$PATH:/usr/local/cuda-9.0/bin"
```

然后退出，至此cuda安装完成。

- 5.安装cudNN

使用torch可以不用安装cudNN,此处略过。

- 6.测试

使用如下代码测试

```
import torch
torch.cuda.is_available()
```
如果结果显示True，那么就可以使用了。

![cuda可以用了](https://github.com/sweetice/sweetice.github.io/blob/master/figures/cuda_is_available.png)
