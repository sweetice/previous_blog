---
layout:     post
title:      PPO Debug Experience 
subtitle:   Problems that I debug PPO
date:       2018-12-20
author:     Johnny
header-img: img/post-bg-reinforcement-learning.png
catalog: true
tags:
    - Reinforcement Learning
    - 学习生活
---

# PPO Debug Experience 
Recently, I need to perform PPO in a complex env.  I refer to some code in GitHub, however, I can't grasp their meaning...

After reading [PPO paper]([https://arxiv.org/abs/1707.06347](https://arxiv.org/abs/1707.06347)
), I decided to code by myself. 

I already have some experience writing RL code. After several minutes, I finished the first version with gym-cart-pole-v0. However, that didn't work...

Then I started to check the core algorithm again and again...It's very sad, the code still did not work.

So I suspect whether the agent's interacting with env is right or not...
Then I started to debug the interaction between agent and env. 
Luckily,  I found that the reward(or Gt/advantage) went wrong. So I refer to some papers about advantage such as GAE, TRPO and so on...

Then I changed the way reward is calculated. The code work.
You can click [here](https://github.com/sweetice/Deep-reinforcement-learning-with-pytorch/tree/master/Char5%20PPO) to ref my code.

