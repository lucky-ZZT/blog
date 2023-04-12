---
title: blog操作日志
abbrlink: '712e1829'
date: 2023-04-11 15:26:29
tags: 日志
cover:
---

## 2023/4/11/

{% tip success%}

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

​	重新在下载主题，替换原文件后——依旧不起作用

​	删除浏览器缓存后——成功修复

​	归因于pwa缓存bug太多了，这里选择直接关了

{% tip success %}

2、修改电子钟显示地区问题

{% endtip %}

​	修改经纬度

```
rectangle: 104.06,30.67 # 获取访问者位置失败时会显示该位置的天气，同时该位置为开启default_rectangle后的位置
```

​	显示依旧存在问题——输入命名{% span red, gulp %}后解决（正常显示）

## 2023/4/12/

{% tip success%}

1、清理掉github贡献图的残留影响

{% endtip %}

我们在平时运用的时候一般用 npm i 来代替 npm install（为npm i 的简写）

但是在实际应用中两者是有些不同的（查阅总结）：

1.使用npm i 安装的模块和依赖，使用npm uninstall是无法删除的，必须使用 npm uninstall i 才可以删除。

2.npm i 会帮助检测 和 当前 node 最匹配的 npm 版本号，并匹配出相互依赖的npm 包应该升级的版本号。

3.npm i 安装的一些包，在当前的node版本下是没有办法使用的，必须使用建议版本。

4.npm  i 安装出现问题是不会出现 npm-debug.log 文件的，但是 npm  install 安装出现问题是有这个文件的。

