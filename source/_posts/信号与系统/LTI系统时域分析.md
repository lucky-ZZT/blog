---
title: LTI系统时域分析
abbrlink: '30782917'
date: 2023-05-15 15:06:23
tags:
swiper_index: 
category: 信号与系统
keywords: 
cover:
highlight_shrink:
---

## 微分方程求解

齐通加非齐特

![微分方程求解2023-05-15 150850](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%B1%82%E8%A7%A32023-05-15%20150850.png)

例题：

![微分方程求解2023-05-15 160910](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%B1%82%E8%A7%A32023-05-15%20160910.png)



## 零输入和零状态响应

### 连续函数初始值

- 初始值：是n阶系统在t=0时接入激励，其响应在t=0+时刻的值，即
  $$
  y^{(j)}(0_+) (j=0,1,2…，n-1)。
  $$
  

- 初始状态：是指系统在激励尚未接入的t=0-时刻的响应值`$y^{(j)}(0_-)$`，该值反映了系统的历史情况，而与激励无关



### 零输入响应

系统只有齐次解，没有特解

![零输入响应12023-05-15 161617](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E9%9B%B6%E8%BE%93%E5%85%A5%E5%93%8D%E5%BA%9412023-05-15%20161617.png)

例题：

![零输入响应22023-05-15 161627](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E9%9B%B6%E8%BE%93%E5%85%A5%E5%93%8D%E5%BA%9422023-05-15%20161627.png)



### 零状态响应

- 初始值确定

![零状态12023-05-15 162243](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E9%9B%B6%E7%8A%B6%E6%80%8112023-05-15%20162243.png)

例题：

![零状态22023-05-15 162257](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E9%9B%B6%E7%8A%B6%E6%80%8122023-05-15%20162257.png)

![零状态3‘2023-05-15 162304](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E9%9B%B6%E7%8A%B6%E6%80%813%E2%80%982023-05-15%20162304.png)

上述问题：可以使用冲激函数匹配法求零输入的初始值

![跳变量2023-05-15 164001](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E8%B7%B3%E5%8F%98%E9%87%8F2023-05-15%20164001.png)





## 单位冲激响应和单位阶跃响应

- 冲激响应

  冲激响应是由单位冲激函数δ(t)所引起的零状态响应，记为h(t)。

  基本信号：冲激函数δ(t)
  基本响应：冲激响应h(t)

  h(t)隐含的条件：

  - f(t)=δ(t)

  - h(0-)=h’(0-)=0 (对二阶系统)

    

- 阶跃响应

  阶跃响应是由单位阶跃函数ε(t)所引起的零状态响应，记为g(t)。基本信号：阶跃函数ε(t) 
  基本响应：阶跃响应g(t)g(t)

  隐含的条件：

  - f(t) = ε(t) 
  - g(0-) = g’(0-) = 0
    

例题：

![例题12023-05-15 165118](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E4%BE%8B%E9%A2%9812023-05-15%20165118.png)

## 卷积

### 定义背景

- 经典微分方程求解条件：

  确定的输入函数

- 卷积：对任意输入的输出

  ![卷积2023-05-15 181839](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%8D%B7%E7%A7%AF2023-05-15%20181839.png)

  为了解决传统方法的局限性（信号没有具体的函数表达式），如上图所示，将信号分成若干的小矩形（一系列冲激信号之和），公式如下：
  $$
  f(t) = \int\limits_{-∞}^{∞}f(τ)\delta(t-τ)dτ
  $$
  通过上述公式：就可以将任意信号，表示为冲激形式，对应着冲激响应。根据线性和时不变性，就能的到任意输入的输出。产生响应如下：
  $$
  f(t) = \int\limits_{-∞}^{∞}f(τ)h(t-τ)dτ
  $$
  因此定义卷积公式如下：
  $$
  r(t) = f(t)*h(t) =f(t) = \int\limits_{-∞}^{∞}f(τ)h(t-τ)dτ
  $$
  

  
