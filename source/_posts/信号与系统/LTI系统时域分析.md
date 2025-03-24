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

## 电路图建立微分方程

![电路图建立微分方程2023-05-15 225508](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E7%94%B5%E8%B7%AF%E5%9B%BE%E5%BB%BA%E7%AB%8B%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B2023-05-15%20225508.png)

根据上图先了解，我们后续所说的微分方程的意义（为什么要解微分方程）



## 微分方程求解

齐通加非齐特

![微分方程求解2023-05-15 150850](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%B1%82%E8%A7%A32023-05-15%20150850.png)

例题：

![微分方程求解2023-05-15 160910](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%BE%AE%E5%88%86%E6%96%B9%E7%A8%8B%E6%B1%82%E8%A7%A32023-05-15%20160910.png)



## 微分算子（解微分方程）

- 定义

![微分算子2023-05-19 103519](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%BE%AE%E5%88%86%E7%AE%97%E5%AD%902023-05-19%20103519.png)

例题：

![例题2023-05-19 103638](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E4%BE%8B%E9%A2%982023-05-19%20103638.png)

- 微分算子性质

  ![性质12023-05-19 103719](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E6%80%A7%E8%B4%A812023-05-19%20103719.png)

  ![性质22023-05-19 103726](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E6%80%A7%E8%B4%A822023-05-19%20103726.png)

  性质四：后积分的话存在常数项，所以不能直接消除

  

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

  为了解决传统方法的局限性（信号没有具体的函数表达式），如上图所示，将信号分成若干的小矩形（通过微分等效为一系列冲激信号之和），公式如下：
  $$
  f(t) = \int\limits_{-∞}^{∞}f(τ)\delta(t-τ)dτ
  $$
  通过上述公式：就可以将任意信号，表示为冲激形式，对应着冲激响应。根据线性和时不变性，就能的到任意输入的输出。产生响应如下：
  $$
  f(t) = \int\limits_{-∞}^{∞}f(τ)h(t-τ)dτ
  $$
  因此定义卷积公式如下：
  $$
  r(t) = f(t)*h(t) = \int\limits_{-∞}^{∞}f(τ)h(t-τ)dτ
  $$

易混点个人理解：

​	首先在公式定义时，明显看到冲激函数的自变量是t(以此为根据做位移)；但在后续的解答过程中，通常把公式理解h先翻转再右移，（此时的自变量已经是τ了）



### 卷积性质与计算

- 性质

![卷积性质2023-05-16 104820](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%8D%B7%E7%A7%AF%E6%80%A7%E8%B4%A82023-05-16%20104820.png)

- 常用公式

  ![常用卷积公式2023-05-16 111422](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%B8%B8%E7%94%A8%E5%8D%B7%E7%A7%AF%E5%85%AC%E5%BC%8F2023-05-16%20111422.png)

- 计算：

![卷积计算2023-05-16 105917](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%8D%B7%E7%A7%AF%E8%AE%A1%E7%AE%972023-05-16%20105917.png)

![卷积计算2023-05-16 110501](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%8D%B7%E7%A7%AF%E8%AE%A1%E7%AE%972023-05-16%20110501.png)



### 卷积图解法

![图解法2023-05-16 110847](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%9B%BE%E8%A7%A3%E6%B3%952023-05-16%20110847.png)

![卷积计算2023-05-16 111059](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%8D%B7%E7%A7%AF%E8%AE%A1%E7%AE%972023-05-16%20111059.png)



## 离散信号分析

### 差分方程

- 差分定义

  ![差分定义2023-05-16 164927](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%B7%AE%E5%88%86%E5%AE%9A%E4%B9%892023-05-16%20164927.png)

![差分定义22023-05-16 165059](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%B7%AE%E5%88%86%E5%AE%9A%E4%B9%8922023-05-16%20165059.png)

- 差分方程

  ![差分方程2023-05-16 165452](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B2023-05-16%20165452.png)

### 差分方程的解

- 差分方程的齐次解

![2023-05-16 170018](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023-05-16%20170018.png)

- 差分方程的特解

![2023-05-16 165928](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023-05-16%20165928.png)

- 全解

  齐次解加特解



例题：

![差分方程例题2023-05-16 170731](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E4%BE%8B%E9%A2%982023-05-16%20170731.png)

### 零输入响应

![零输入响应2023-05-16 170858](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E9%9B%B6%E8%BE%93%E5%85%A5%E5%93%8D%E5%BA%942023-05-16%20170858.png)

### 零状态响应

![零状态响应2023-05-16 171002](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E9%9B%B6%E7%8A%B6%E6%80%81%E5%93%8D%E5%BA%942023-05-16%20171002.png)

例题：

![例题、2023-05-18 112130](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E4%BE%8B%E9%A2%98%E3%80%812023-05-18%20112130.png)



### 单位序列响应和单位阶跃响应

针对f(k)无规律的情况，如何求响应。

- 单位序列响应

![单位序列](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/%E5%8D%95%E4%BD%8D%E5%BA%8F%E5%88%97.png)
