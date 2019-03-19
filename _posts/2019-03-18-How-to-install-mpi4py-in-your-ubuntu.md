---
layout:     post
title:      How to installation mpi4py in your ubuntu
subtitle:   Enjoy parallel computation!
date:       2019-03-18
author:     Johnny
header-img: img/post_bao_yan.jpg
catalog: true
tags:
    - 杂
---


#　How to install mpi4py in your ubuntu computer


首先要说明的是，直接使用pip　安装并不可取．

## １．安装openmpi

- 1.1 下载
URL: http://www.open-mpi.org/software/ompi/v1.10/

```
wget https://www.open-mpi.org/software/ompi/v1.10/downloads/openmpi-1.10.2.tar.gz
tar xvzf openmpi-1.10.x.tar.gz
cd openmpi-xxx/
```

- 1.2 编译安装

首先编译:  
```
./configure
```

注意：不要使用  
```
bash ./configure
```

接下来安装:
```
sudo make all install
```


注意:这里必须要使用sudo,否则会提示你权限不足

- 1.3 添加环境变量

进入~目录后
```
sudo gedit .bashrc
```

在最后一行添加上:
```
#mpi4py
export LD_LIBRARY_PATH+=:/usr/local/lib
```

激活一下:  
```
source /etc/profile
```

- 1.4 进行测试

```
cd openmpi-1.10.2/examples
make
mpirun -np 4 hello_c
```

当你的电脑上面显示:
```
Hello, world, I am 0 of 4, (Open MPI v1.10.2, package: Open MPI mirror@agent Distribution, ident: 1.10.2, repo rev: v1.10.1-145-g799148f, Jan 21, 2016, 123)
Hello, world, I am 2 of 4, (Open MPI v1.10.2, package: Open MPI mirror@agent Distribution, ident: 1.10.2, repo rev: v1.10.1-145-g799148f, Jan 21, 2016, 123)
Hello, world, I am 3 of 4, (Open MPI v1.10.2, package: Open MPI mirror@agent Distribution, ident: 1.10.2, repo rev: v1.10.1-145-g799148f, Jan 21, 2016, 123)
Hello, world, I am 1 of 4, (Open MPI v1.10.2, package: Open MPI mirror@agent Distribution, ident: 1.10.2, repo rev: v1.10.1-145-g799148f, Jan 21, 2016, 123)

```
这就说明openmpi安装好了.

## 2. 安装mpi4py

```
pip install mpi4py
```

出现一下信息:
```
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting mpi4py
  Using cached https://pypi.tuna.tsinghua.edu.cn/packages/55/a2/c827b196070e161357b49287fa46d69f25641930fd5f854722319d431843/mpi4py-3.0.1.tar.gz
Building wheels for collected packages: mpi4py
  Building wheel for mpi4py (setup.py) ... done
  Stored in directory: /home/mirror/.cache/pip/wheels/73/ef/7a/e81433083a06d8735f0b50e1e388168b39b88444fd81fe5f27
Successfully built mpi4py
Installing collected packages: mpi4py
Successfully installed mpi4py-3.0.1
You are using pip version 19.0.2, however version 19.0.3 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.

```
这就说明mpi4py也安装好了.
