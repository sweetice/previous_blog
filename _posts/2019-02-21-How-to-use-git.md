---
layout:     post
title:      How to use git 
subtitle:   Enjoy git 
date:       2019-02-21
author:     Johnny
header-img: img/post_bao_yan.jpg
catalog: true
tags:
    - 杂
---


# git提效工具的简单使用

这篇博客介绍git工具如何使用。git的好处我不必多做介绍，git是一个提效神器，当你：

- 使用v1，v2来管理你的代码
- 多人协作写代码
- 想要避免在web端修改代码

这个时候你都应该学习一下如何使用git了。

## git的安装

```
sudo apt install git

```

## 管理已经存在的repo

这里我以我的[强化学习教程](https://github.com/sweetice/Deep-reinforcement-learning-with-pytorch)为例子。

0. 初始化git
选择一个本地文件夹，用来存放repo。选择好之后，使用命令行进入这个目录，然后添加自己的信息.注意，你的名字和邮箱是必要的。

```
$ git config --global user.name "sweetice"
```

```
$ git config --global user.email "269401927@qq.com"
```

接下来初始化

```
git init
```
1. 首先，将你的repo复制到本地。
![Fig.1 Clone repo](https://github.com/sweetice/sweetice.github.io/blob/master/figures/clone_repo.png)

```
$ git clone  https://github.com/sweetice/Deep-reinforcement-learning-with-pytorch.git
```

静静地等着复制完成就好。

这里有一个查看本地repo来源的小技巧
```
$ git remote -v
```

这样子，就会显示你的repo的来源

> https://github.com/sweetice/Deep-reinforcement-learning-with-pytorch.git

2. 提交修改

你把代码下载到了本地，进行了一些修改，这个时候你觉得比较满意了，可以提交了。首先需要在本地产生提交的信息。提交信息分为N步。

- 1)把修改的文件包括进来
```
$ git add helloworld.py
```

当你修改的文件比较多时，可以
```
$ git add .
```

- 2) 提交commit

```
$ git commit -m "helloworld"
```

注意，引号里面的内容选填，你填写的内容将在网页端显示出来。

- 3) 上传到web端口

```
$ git push -u origin master
```



## 写在最后-问题与解决方案

### 本地端修改之后，无法推送到web端

**问题描述**
```
(base) mirror@agent:~/Documents/GithubCode$ git push -u origin master
error: src refspec master does not match any.
error: failed to push some refs to 'https://github.com/sweetice/Deep-reinforcement-learning-with-pytorch.git'
```

由于之前错误的嵌套了web端的repo，造成了问题。

**解决方案**
- 提交一下
```
$ git add .
```
出现提示信息
```
warning: adding embedded git repository: Deep-reinforcement-learning-with-pytorch
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint: 
hint: 	git submodule add <url> Deep-reinforcement-learning-with-pytorch
hint: 
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint: 
hint: 	git rm --cached Deep-reinforcement-learning-with-pytorch
hint: 
hint: See "git help submodule" for more information.

```
-  强制删除嵌套

```
$ git rm --cached Deep-reinforcement-learning-with-pytorch/ -f

```

问题解决。

出现问题的原因还有：

-1. 本地git仓库目录下为空

-2. 本地仓库add后未commit

-3. git init错误

对应的解决方案：
-1. 打开隐藏文件和文件夹显示

-2. 到本地仓库目录下查看是否有.git文件夹——无 则git init

-3. 看.git文件夹下是否有之前提交的文件——若无 则重新 git commit (如果之前git add过的话 没有就要重新 add commit)

### push之后，web端代码没有发生改变。

**问题描述**
使用如下命令，成功将本地代码推送至了web端口

```
$ git push -u origin master
```

但是web端没有发生变化。

**解决方案**

这是由于没有add 和commit引起的，直接add 和 commit就可以了

```
$ git add .
```

```
$ git commit -m "add some new algorithms"
```

之后再
```
$ git push -u origin master
```
