---
layout:     post
title:      How to access google, wikipedia .etc in mainland China with IPV6
subtitle:   Enjoy Internet without GFW
date:       2018-12-08
author:     Johnny
header-img: img/post_bao_yan.jpg
catalog: true
tags:
    - 杂
---

# How to access google, Wikipedia .etc in mainland China

If you are in ipv6 environments, you can't access google, facebook, youtube directly. You should change your hosts file.

In this article, we argue that how to access google, facebook, youtube with ipv6.

## Download hosts file from github

Click [here](https://github.com/lennylxx/ipv6-hosts) to visit github pages. If you can't, you can paste *https://github.com/lennylxx/ipv6-hosts* to your browser.

And then should download the file that I marked with a red square.

![hosts that you should download](http://upload-images.jianshu.io/upload_images/7814231-1a7e960f4f494980.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## Replace origin hosts with a new one.

If you are a Linux user.
You can use the follow  code to edit hosts file:

```
$  sudo gedit /etc/hosts
```

Then you should paste the contents of new hosts into the old file.

Last but not least, you should restart your network...
 
```
$ sudo /etc/init.d/networking restart
```
Enjoy yourself : )
