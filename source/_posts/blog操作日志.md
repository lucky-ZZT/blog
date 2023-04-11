---
title: blog操作日志
abbrlink: '712e1829'
date: 2023-04-11 15:26:29
tags:
---

## 2023/4/11/-15:30

{% tip error %}

1、针对代码块显示问题 未能操作成功！

{% endtip %}

​	试图使用butterfly的代码高度限制

```
highlight_height_limit: false # unit: px
```

​	使用代码框展开功能代替

```
highlight_shrink: true #代码框不展开，需点击 '>' 打开
```

{% tip success %}

2、修改电子钟显示地区问题

{% endtip %}

​	修改经纬度

```
rectangle: 104.06,30.67 # 获取访问者位置失败时会显示该位置的天气，同时该位置为开启default_rectangle后的位置
```

​	显示依旧存在问题——输入命名{% span red, gulp %}后解决（正常显示）



