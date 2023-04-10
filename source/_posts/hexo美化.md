---
title: hexo美化
abbrlink: bd46f10a
date: 2023-04-10 13:46:22
tags:
---

>转录自：[安知鱼](https://anzhiy.cn/posts/sdxhu.html)

## 安装 Butterfly

>参考教程: [https://butterfly.js.org/posts/21cfbf15/#%E5%AE%89%E8%A3%9D](https://butterfly.js.org/posts/21cfbf15/#安裝)
>
>```
>git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
>```
>
>==注意事项==
>
>​	主题在上传至github时，一定要删除.git文件

## 修改主题配置

>[主题修改导航](https://butterfly.js.org/posts/4aa8abbe/#導航菜單)主题新手引导
>
>建议修改方法：在根目录新建==_config.butterfly.yml==，将主题中的配置文件复制到该文件中。之后就可以直接在该文件中修改配置，降低版本更新带来的影响
>
>主题文件：关键词，名称等不再细述

## 配置文章链接转数字或字母

>参考: https://github.com/rozbo/hexo-abbrlink
>
>```
>npm install hexo-abbrlink --save
>```
>
>将文章装换为下述格式（.html），方便引用
>
>​	http://localhost:4000/posts/359ff663.html

## 本地搜索依赖

>参考：https://github.com/wzpan/hexo-generator-search
>
>```
>npm install hexo-generator-search --save
>```

## live2d(桌宠)

>```
># 安装live2d
>npm install --save hexo-helper-live2d
># 安装模型
>npm install --save live2d-widget-model-koharu
>```
>
>参考：https://github.com/EYHN/hexo-helper-live2d

## sitemap

>```
>BASHnpm install hexo-generator-sitemap --save
>npm install hexo-generator-baidu-sitemap --save-dev
>```
>
>方便爬虫

>## Rss
>
>```
>npm install hexo-generator-feed --save
>```
>
>方便爬虫

## 百度主动推送

>参考：https://github.com/huiwang/hexo-baidu-url-submit
>
>```
>npm install hexo-baidu-url-submit --save
>```
>
>主动推送Hexo博客新链接至百度搜索引擎
