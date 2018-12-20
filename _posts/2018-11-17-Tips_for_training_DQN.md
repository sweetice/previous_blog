---
layout:     post
title:      Tips for training DQN/AC algorithm in Reinforcement learning
subtitle:   训练DQN/AC算法的技巧
date:       2018-11-16
author:     Johnny
header-img: img/post-bg-reinforcement-learning.png
catalog: true
tags:
    - Reinforcement Learning
---

# Tips for training AC algorithm in Reinforcement learning

在强化学习中训练AC算法的技巧。

笔者最近做了大量经典强化学习算法复现的工作，在复现的过程中也遇到了大量的坑。为了解决这些坑，我积累了一些经验。为了方便日后查阅，我记录在这一篇博客里。

**本博客长期更新**

## Tips for training DQN

首先讲一个我碰到的让我头疼了很长时间的问题。

### DQN中loss很小，网络却不收敛

首先我们做一个分析

> A = Q - V 

由于长时间得不到奖励，Q，V算出来都趋向于0，他们的差A也趋向于0，这样子就导致loss也趋向于0，所以就出现了一种让初学者难以想象的情况：

**loss非常小，逼近于0，但网络就是不收敛。**

造成这种现象的原因还有：gamma值设置的太大。对于随机探索要上万步才能达到最优解的情况，通常gamma设置为0.995以上比较好。

### DQN中loss非常大，但网络开始有收敛的迹象

我们回顾一下DQN中loss计算的方法

> A = Q - V


Q是由 target_net生成， V是由act_net生成。所以，当两个网络相差太大时，会出现loss非常大的情况（笔者在训练时出现过1e13的情况）。

那么我们需要解决的就是使两个网络差距不要太大。

解决的方案有：

- batch_size 不要太大， 64为宜。

如果是对loss求和，那么大的batch_size意味着大的loss。

- 更新的频率要适中，对于小型任务（如CartPole），最好训练十次左右就更新target_net

更新频率太低，那么两个网络相差巨大，由于NN的非线性单元的存在，参数空间的微小变化，将导致输出空间产生巨大的变化。


## memory的设计问题

DQN有两个非常有意思的点。一个是两个网络的设计，另是一个是经验回放池。
在设计memory中，一定要注意设计的memory的capacity需要足够的大。这个capacity的下界是至少需要将reward囊括进来。

对于sparse reward task，capacity大小很可能直接决定网络是否收敛！

## AC方法设计的一般问题

AC框架是非常重要的强化学习方法，现代的算法几乎都是基于AC框架的。由于AC框架既有Policy Gradient，又有Q-learning，AC框架调参难度相比起单一的PG/Q 方法更加难以调整。经验在这里变得非常重要。

对于AC框架，我们一般先会去调Q-learning部分，不管是A2C，A3C还是PPO，Q-learning部分（也就是critic）收敛之后，再去调整actor部分，这样子调参会好得多。

 Actor-critic 方法非常依赖工程师的经验，在经典的CartPole环境中，设置一个隐藏层的网络稳定性会比两个隐藏层问题，设置32个units会比128个稳定得多。
如何设计稳定、可靠的神经网络呢？目前还没有什么标准，这个只依赖于工程师的经验了。
强化学习比起深度学习，更像是炼丹。有的时候随机种子对收敛性有决定性的影响。

****

**未完待续...**
