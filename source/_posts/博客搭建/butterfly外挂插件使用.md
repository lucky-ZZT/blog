---
title: butterfly外挂插件使用
abbrlink: 89381aa1
date: 2023-04-10 17:39:52
tags: 外挂标签
cover:
category: 博客搭建
---

>转载自：https://akilar.top/posts/615e2dec/
>
>官方相关文档：https://butterfly.js.org/posts/4aa8abbe/#timeline



## 分栏tab

{% tabs tab %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

>```
>{% tabs test3, -1 %}
><!-- tab -->
>**This is Tab 1.**
><!-- endtab -->
>
><!-- tab -->
>**This is Tab 2.**
><!-- endtab -->
>
><!-- tab -->
>**This is Tab 3.**
><!-- endtab -->
>{% endtabs %}
>```

## tab-hide

{% tabs test1.1 %}
<!-- tab lnline -->
inline 在文本里面添加按钮隐藏内容，只限文字

( content不能包含英文逗号，可用&sbquo;)

``` {% hideInline content,display,bg,color %} ```

- content: 文本内容

- display: 按钮显示的文字(可选)

- bg: 按钮的背景颜色(可选)

- color: 按钮文字的颜色(可选)
  <!-- endtab -->

<!-- tab Block -->
block独立的block隐藏内容，可以隐藏很多内容，包括图片，代码块等等

( display 不能包含英文逗号，可用&sbquo;)

```
{% hideBlock display,bg,color %}
content
{% endhideBlock %}
```

- content: 文本内容

- display: 按钮显示的文字(可选)

- bg: 按钮的背景颜色(可选)

- color: 按钮文字的颜色(可选)

<!-- endtab -->

<!-- tab Toggle -->
如果你需要展示的内容太多，可以把它隐藏在收缩框里，需要时再把它展开。

( display 不能包含英文逗号，可用&sbquo;)

```
{% hideToggle display,bg,color %}
content
{% endhideToggle %}
```

- content: 文本内容

- display: 按钮显示的文字(可选)

- bg: 按钮的背景颜色(可选)

- color: 按钮文字的颜色(可选)

<!-- endtab -->
{% endtabs %}

## 行内文本样式text
{% tabs test2 %}
<!-- tab 样式预览 -->
1. 带 {% u 下划线 %} 的文本
2. 带 {% emp 着重号 %} 的文本
3. 带 {% wavy 波浪线 %} 的文本
4. 带 {% del 删除线 %} 的文本
5. 键盘样式的文本 {% kbd command %} + {% kbd D %}
6. 密码样式的文本：{% psw 这里没有验证码 %}
<!-- endtab -->

<!-- tab 源码 -->

```
1. 带 {% u 下划线 %} 的文本
2. 带 {% emp 着重号 %} 的文本
3. 带 {% wavy 波浪线 %} 的文本
4. 带 {% del 删除线 %} 的文本
5. 键盘样式的文本 {% kbd command %} + {% kbd D %}
6. 密码样式的文本：{% psw 这里没有验证码 %}
```

<!-- endtab -->

{% endtabs %}

## 行内文本 span

{% tabs span %}
<!-- tab 样式预览 -->

- 彩色文字
在一段话中方便插入各种颜色的标签，包括：{% span red, 红色 %}、{% span yellow, 黄色 %}、{% span green, 绿色 %}、{% span cyan, 青色 %}、{% span blue, 蓝色 %}、{% span gray, 灰色 %}。
- 超大号文字
文档「开始」页面中的标题部分就是超大号文字。
{% span center logo large, Volantis %}
{% span center small, A Wonderful Theme for Hexo %}

<!-- endtab -->

<!-- tab 源码 -->

```
- 彩色文字
在一段话中方便插入各种颜色的标签，包括：{% span red, 红色 %}、{% span yellow, 黄色 %}、{% span green, 绿色 %}、{% span cyan, 青色 %}、{% span blue, 蓝色 %}、{% span gray, 灰色 %}。
- 超大号文字
文档「开始」页面中的标题部分就是超大号文字。
{% span center logo large, Volantis %}
{% span center small, A Wonderful Theme for Hexo %}
```

<!-- endtab -->

{% endtabs %}

## 段落文本 p

{% tabs test4 %}
<!-- tab 样式预览 -->

- 彩色文字
在一段话中方便插入各种颜色的标签，包括：{% p red, 红色 %}、{% p yellow, 黄色 %}、{% p green, 绿色 %}、{% p cyan, 青色 %}、{% p blue, 蓝色 %}、{% p gray, 灰色 %}。
- 超大号文字
文档「开始」页面中的标题部分就是超大号文字。
{% p center logo large, Volantis %}
{% p center small, A Wonderful Theme for Hexo %}

<!-- endtab -->

<!-- tab 源码 -->

```
- 彩色文字
在一段话中方便插入各种颜色的标签，包括：{% p red, 红色 %}、{% p yellow, 黄色 %}、{% p green, 绿色 %}、{% p cyan, 青色 %}、{% p blue, 蓝色 %}、{% p gray, 灰色 %}。
- 超大号文字
文档「开始」页面中的标题部分就是超大号文字。
{% p center logo large, Volantis %}
{% p center small, A Wonderful Theme for Hexo %}
```

<!-- endtab -->

{% endtabs %}

## 引用 note

{% tabs test5 %}
<!-- tab 样式预览 -->

{% hideToggle 方式一,dg,color %}

1. `simple`样式
{% note simple %}默认 提示块标签{% endnote %}
   
   {% note default simple %}default 提示块标签{% endnote %}

   {% note primary simple %}primary 提示块标签{% endnote %}

   {% note success simple %}success 提示块标签{% endnote %}

   {% note info simple %}info 提示块标签{% endnote %}

   {% note warning simple %}warning 提示块标签{% endnote %}

   {% note danger simple %}danger 提示块标签{% endnote %}

2. `modern`样式
{% note modern %}默认 提示块标签{% endnote %}
   
   {% note default modern %}default 提示块标签{% endnote %}

   {% note primary modern %}primary 提示块标签{% endnote %}

   {% note success modern %}success 提示块标签{% endnote %}

   {% note info modern %}info 提示块标签{% endnote %}

   {% note warning modern %}warning 提示块标签{% endnote %}

   {% note danger modern %}danger 提示块标签{% endnote %}

3. `flat`样式
{% note flat %}默认 提示块标签{% endnote %}
   
   {% note default flat %}default 提示块标签{% endnote %}

   {% note primary flat %}primary 提示块标签{% endnote %}

   {% note success flat %}success 提示块标签{% endnote %}

   {% note info flat %}info 提示块标签{% endnote %}

   {% note warning flat %}warning 提示块标签{% endnote %}

   {% note danger flat %}danger 提示块标签{% endnote %}

4. `disabled`样式
{% note disabled %}默认 提示块标签{% endnote %}
   
   {% note default disabled %}default 提示块标签{% endnote %}

   {% note primary disabled %}primary 提示块标签{% endnote %}

   {% note success disabled %}success 提示块标签{% endnote %}

   {% note info disabled %}info 提示块标签{% endnote %}

   {% note warning disabled %}warning 提示块标签{% endnote %}

   {% note danger disabled %}danger 提示块标签{% endnote %}

5. `no-icon`样式
   {% note no-icon %}默认 提示块标签{% endnote %}
   
   {% note default no-icon %}default 提示块标签{% endnote %}

   {% note primary no-icon %}primary 提示块标签{% endnote %}

   {% note success no-icon %}success 提示块标签{% endnote %}

   {% note info no-icon %}info 提示块标签{% endnote %}

   {% note warning no-icon %}warning 提示块标签{% endnote %}

   {% note danger no-icon %}danger 提示块标签{% endnote %}

{% endhideToggle %}

{% hideToggle 方式2,bg,color %}

1. `simple`样式

   {% note 'fab fa-cc-visa' simple %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note blue 'fas fa-bullhorn' simple %}2021年快到了....{% endnote %}

   {% note pink 'fas fa-car-crash' simple %}小心开车 安全至上{% endnote %}

   {% note red 'fas fa-fan' simple%}这是三片呢？还是四片？{% endnote %}

   {% note orange 'fas fa-battery-half' simple %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note purple 'far fa-hand-scissors' simple %}剪刀石头布{% endnote %}

   {% note green 'fab fa-internet-explorer' simple %}前端最讨厌的浏览器{% endnote %}

2. `modern`样式

   {% note 'fab fa-cc-visa' modern %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note blue 'fas fa-bullhorn' modern %}2021年快到了....{% endnote %}

   {% note pink 'fas fa-car-crash' modern %}小心开车 安全至上{% endnote %}

   {% note red 'fas fa-fan' modern%}这是三片呢？还是四片？{% endnote %}

   {% note orange 'fas fa-battery-half' modern %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note purple 'far fa-hand-scissors' modern %}剪刀石头布{% endnote %}

   {% note green 'fab fa-internet-explorer' modern %}前端最讨厌的浏览器{% endnote %}

3. `flat`样式

   {% note 'fab fa-cc-visa' flat %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note blue 'fas fa-bullhorn' flat %}2021年快到了....{% endnote %}

   {% note pink 'fas fa-car-crash' flat %}小心开车 安全至上{% endnote %}

   {% note red 'fas fa-fan' flat%}这是三片呢？还是四片？{% endnote %}

   {% note orange 'fas fa-battery-half' flat %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note purple 'far fa-hand-scissors' flat %}剪刀石头布{% endnote %}

   {% note green 'fab fa-internet-explorer' flat %}前端最讨厌的浏览器{% endnote %}

4. `disabled`样式

   {% note 'fab fa-cc-visa' disabled %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note blue 'fas fa-bullhorn' disabled %}2021年快到了....{% endnote %}

   {% note pink 'fas fa-car-crash' disabled %}小心开车 安全至上{% endnote %}

   {% note red 'fas fa-fan' disabled %}这是三片呢？还是四片？{% endnote %}

   {% note orange 'fas fa-battery-half' disabled %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note purple 'far fa-hand-scissors' disabled %}剪刀石头布{% endnote %}

   {% note green 'fab fa-internet-explorer' disabled %}前端最讨厌的浏览器{% endnote %}

5. `no-icon`样式

   {% note no-icon %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note blue no-icon %}2021年快到了....{% endnote %}

   {% note pink no-icon %}小心开车 安全至上{% endnote %}

   {% note red no-icon %}这是三片呢？还是四片？{% endnote %}

   {% note orange no-icon %}你是刷 Visa 还是 UnionPay{% endnote %}

   {% note purple no-icon %}剪刀石头布{% endnote %}

   {% note green no-icon %}前端最讨厌的浏览器{% endnote %}

{% endhideToggle %}

<!-- endtab -->

<!-- tab 源码 -->

{% hideToggle 方式一,dg,color %}

1. `simple`样式

   ```
   MARKDOWN
   {% note simple %}默认 提示块标签{% endnote %}
   
   {% note default simple %}default 提示块标签{% endnote %}
   
   {% note primary simple %}primary 提示块标签{% endnote %}
   
   {% note success simple %}success 提示块标签{% endnote %}
   
   {% note info simple %}info 提示块标签{% endnote %}
   
   {% note warning simple %}warning 提示块标签{% endnote %}
   
   {% note danger simple %}danger 提示块标签{% endnote %}
   ```

2. `modern`样式

   ```
   MARKDOWN
   {% note modern %}默认 提示块标签{% endnote %}
   
   {% note default modern %}default 提示块标签{% endnote %}
   
   {% note primary modern %}primary 提示块标签{% endnote %}
   
   {% note success modern %}success 提示块标签{% endnote %}
   
   {% note info modern %}info 提示块标签{% endnote %}
   
   {% note warning modern %}warning 提示块标签{% endnote %}
   
   {% note danger modern %}danger 提示块标签{% endnote %}
   ```

3. `flat`样式

   ```
   MARKDOWN
   {% note flat %}默认 提示块标签{% endnote %}
   
   {% note default flat %}default 提示块标签{% endnote %}
   
   {% note primary flat %}primary 提示块标签{% endnote %}
   
   {% note success flat %}success 提示块标签{% endnote %}
   
   {% note info flat %}info 提示块标签{% endnote %}
   
   {% note warning flat %}warning 提示块标签{% endnote %}
   
   {% note danger flat %}danger 提示块标签{% endnote %}
   ```

4. `disabled`样式

   ```
   MARKDOWN
   {% note disabled %}默认 提示块标签{% endnote %}
   
   {% note default disabled %}default 提示块标签{% endnote %}
   
   {% note primary disabled %}primary 提示块标签{% endnote %}
   
   {% note success disabled %}success 提示块标签{% endnote %}
   
   {% note info disabled %}info 提示块标签{% endnote %}
   
   {% note warning disabled %}warning 提示块标签{% endnote %}
   
   {% note danger disabled %}danger 提示块标签{% endnote %}
   ```

5. `no-icon`样式

   ```
   MARKDOWN
   {% note no-icon %}默认 提示块标签{% endnote %}
   
   {% note default no-icon %}default 提示块标签{% endnote %}
   
   {% note primary no-icon %}primary 提示块标签{% endnote %}
   
   {% note success no-icon %}success 提示块标签{% endnote %}
   
   {% note info no-icon %}info 提示块标签{% endnote %}
   
   {% note warning no-icon %}warning 提示块标签{% endnote %}
   
   {% note danger no-icon %}danger 提示块标签{% endnote %}
   ```

{% endhideToggle %}

{% hideToggle 方式2,bg,color %}

1. `simple`样式

   ```
   MARKDOWN
   {% note 'fab fa-cc-visa' simple %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note blue 'fas fa-bullhorn' simple %}2021年快到了....{% endnote %}
   
   {% note pink 'fas fa-car-crash' simple %}小心开车 安全至上{% endnote %}
   
   {% note red 'fas fa-fan' simple%}这是三片呢？还是四片？{% endnote %}
   
   {% note orange 'fas fa-battery-half' simple %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note purple 'far fa-hand-scissors' simple %}剪刀石头布{% endnote %}
   
   {% note green 'fab fa-internet-explorer' simple %}前端最讨厌的浏览器{% endnote %}
   ```

2. `modern`样式

   ```
   MARKDOWN
   {% note 'fab fa-cc-visa' modern %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note blue 'fas fa-bullhorn' modern %}2021年快到了....{% endnote %}
   
   {% note pink 'fas fa-car-crash' modern %}小心开车 安全至上{% endnote %}
   
   {% note red 'fas fa-fan' modern%}这是三片呢？还是四片？{% endnote %}
   
   {% note orange 'fas fa-battery-half' modern %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note purple 'far fa-hand-scissors' modern %}剪刀石头布{% endnote %}
   
   {% note green 'fab fa-internet-explorer' modern %}前端最讨厌的浏览器{% endnote %}
   ```

3. `flat`样式

   ```
   MARKDOWN
   {% note 'fab fa-cc-visa' flat %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note blue 'fas fa-bullhorn' flat %}2021年快到了....{% endnote %}
   
   {% note pink 'fas fa-car-crash' flat %}小心开车 安全至上{% endnote %}
   
   {% note red 'fas fa-fan' flat%}这是三片呢？还是四片？{% endnote %}
   
   {% note orange 'fas fa-battery-half' flat %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note purple 'far fa-hand-scissors' flat %}剪刀石头布{% endnote %}
   
   {% note green 'fab fa-internet-explorer' flat %}前端最讨厌的浏览器{% endnote %}
   ```

4. `disabled`样式

   ```
   MARKDOWN
   {% note 'fab fa-cc-visa' disabled %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note blue 'fas fa-bullhorn' disabled %}2021年快到了....{% endnote %}
   
   {% note pink 'fas fa-car-crash' disabled %}小心开车 安全至上{% endnote %}
   
   {% note red 'fas fa-fan' disabled %}这是三片呢？还是四片？{% endnote %}
   
   {% note orange 'fas fa-battery-half' disabled %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note purple 'far fa-hand-scissors' disabled %}剪刀石头布{% endnote %}
   
   {% note green 'fab fa-internet-explorer' disabled %}前端最讨厌的浏览器{% endnote %}
   ```

5. `no-icon`样式

   ```
   MARKDOWN
   {% note no-icon %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note blue no-icon %}2021年快到了....{% endnote %}
   
   {% note pink no-icon %}小心开车 安全至上{% endnote %}
   
   {% note red no-icon %}这是三片呢？还是四片？{% endnote %}
   
   {% note orange no-icon %}你是刷 Visa 还是 UnionPay{% endnote %}
   
   {% note purple no-icon %}剪刀石头布{% endnote %}
   
   {% note green no-icon %}前端最讨厌的浏览器{% endnote %}
   ```

{% endhideToggle %}

<!-- endtab -->

{% endtabs %}

## 上标标签 tip

{% tabs test6 %}
<!-- tab 样式预览 -->

{% tip %}default{% endtip %}
{% tip info %}info{% endtip %}
{% tip success %}success{% endtip %}
{% tip error %}error{% endtip %}
{% tip warning %}warning{% endtip %}
{% tip bolt %}bolt{% endtip %}
{% tip ban %}ban{% endtip %}
{% tip home %}home{% endtip %}
{% tip sync %}sync{% endtip %}
{% tip cogs %}cogs{% endtip %}
{% tip key %}key{% endtip %}
{% tip bell %}bell{% endtip %}
{% tip fa-atom %}自定义font awesome图标{% endtip %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% tip %}default{% endtip %}
{% tip info %}info{% endtip %}
{% tip success %}success{% endtip %}
{% tip error %}error{% endtip %}
{% tip warning %}warning{% endtip %}
{% tip bolt %}bolt{% endtip %}
{% tip ban %}ban{% endtip %}
{% tip home %}home{% endtip %}
{% tip sync %}sync{% endtip %}
{% tip cogs %}cogs{% endtip %}
{% tip key %}key{% endtip %}
{% tip bell %}bell{% endtip %}
{% tip fa-atom %}自定义font awesome图标{% endtip %}
```

<!-- endtab -->

{% endtabs %}

## 动态标签 anima

{% tabs test7 %}
<!-- tab 样式预览 -->

{% tip warning faa-horizontal animated %}

动态标签的实质是引用了[font-awesome-animation](https://github.com/l-lin/font-awesome-animation)的css样式，不一定局限于tip标签，也可以是其他标签。
只不过这里`tip.js`是我自己写的，所以我清楚它会怎么被渲染成html，才用的这个写法。
可以熟读文档，使用html语言来编写其他标签类型。

{% endtip %}

1.On DOM load（当页面加载时显示动画）

{% tip warning faa-horizontal animated %}warning{% endtip %}
{% tip ban faa-flash animated %}ban{% endtip %}

2.调整动画速度

{% tip warning faa-horizontal animated faa-fast %}warning{% endtip %}
{% tip ban faa-flash animated faa-slow %}ban{% endtip %}

3.On hover（当鼠标悬停时显示动画）

{% tip warning faa-horizontal animated-hover %}warning{% endtip %}
{% tip ban faa-flash animated-hover %}ban{% endtip %}

4.On parent hover（当鼠标悬停在父级元素时显示动画）

{% tip warning faa-parent animated-hover %}<p class="faa-horizontal">warning</p>{% endtip %}
{% tip ban faa-parent animated-hover %}<p class="faa-flash">ban</p>{% endtip %}

<!-- endtab -->

<!-- tab 源码 -->

1. On DOM load（当页面加载时显示动画）

   ```
   MARKDOWN
   {% tip warning faa-horizontal animated %}warning{% endtip %}
   {% tip ban faa-flash animated %}ban{% endtip %}
   ```

2. 调整动画速度

   ```
   MARKDOWN
   {% tip warning faa-horizontal animated faa-fast %}warning{% endtip %}
   {% tip ban faa-flash animated faa-slow %}ban{% endtip %}
   ```

3. On hover（当鼠标悬停时显示动画）

   ```
   MARKDOWN
   {% tip warning faa-horizontal animated-hover %}warning{% endtip %}
   {% tip ban faa-flash animated-hover %}ban{% endtip %}
   ```

4. On parent hover（当鼠标悬停在父级元素时显示动画）

   ```
   MARKDOWN
   {% tip warning faa-parent animated-hover %}<p class="faa-horizontal">warning</p>{% endtip %}
   {% tip ban faa-parent animated-hover %}<p class="faa-flash">ban</p>{% endtip %}
   ```

<!-- endtab -->

{% endtabs %}

## 复选列表 checkbox

{% tabs test7 %}
<!-- tab 样式预览 -->

{% checkbox 纯文本测试 %}
{% checkbox checked, 支持简单的 [markdown](https://guides.github.com/features/mastering-markdown/) 语法 %}
{% checkbox red, 支持自定义颜色 %}
{% checkbox green checked, 绿色 + 默认选中 %}
{% checkbox yellow checked, 黄色 + 默认选中 %}
{% checkbox cyan checked, 青色 + 默认选中 %}
{% checkbox blue checked, 蓝色 + 默认选中 %}
{% checkbox plus green checked, 增加 %}
{% checkbox minus yellow checked, 减少 %}
{% checkbox times red checked, 叉 %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% checkbox 纯文本测试 %}
{% checkbox checked, 支持简单的 [markdown](https://guides.github.com/features/mastering-markdown/) 语法 %}
{% checkbox red, 支持自定义颜色 %}
{% checkbox green checked, 绿色 + 默认选中 %}
{% checkbox yellow checked, 黄色 + 默认选中 %}
{% checkbox cyan checked, 青色 + 默认选中 %}
{% checkbox blue checked, 蓝色 + 默认选中 %}
{% checkbox plus green checked, 增加 %}
{% checkbox minus yellow checked, 减少 %}
{% checkbox times red checked, 叉 %}
```

<!-- endtab -->

{% endtabs %}

## 单选列表 radio

{% tabs test8 %}
<!-- tab 样式预览 -->

{% radio 纯文本测试 %}
{% radio checked, 支持简单的 [markdown](https://guides.github.com/features/mastering-markdown/) 语法 %}
{% radio red, 支持自定义颜色 %}
{% radio green, 绿色 %}
{% radio yellow, 黄色 %}
{% radio cyan, 青色 %}
{% radio blue, 蓝色 %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% radio 纯文本测试 %}
{% radio checked, 支持简单的 [markdown](https://guides.github.com/features/mastering-markdown/) 语法 %}
{% radio red, 支持自定义颜色 %}
{% radio green, 绿色 %}
{% radio yellow, 黄色 %}
{% radio cyan, 青色 %}
{% radio blue, 蓝色 %}
```

<!-- endtab -->

{% endtabs %}

## 时间轴 timeline

{% tabs timeline %}
<!-- tab 样式预览 -->

{% timeline 时间轴样式,blue %}

<!-- timeline 2020-07-24 [2.6.6 -> 3.0](https://github.com/volantis-x/hexo-theme-volantis/releases) -->

1. 如果有 `hexo-lazyload-image` 插件，需要删除并重新安装最新版本，设置 `lazyload.isSPA: true`。
2. 2.x 版本的 css 和 js 不适用于 3.x 版本，如果使用了 `use_cdn: true` 则需要删除。
3. 2.x 版本的 fancybox 标签在 3.x 版本中被重命名为 gallery 。
4. 2.x 版本的置顶 `top: true` 改为了 `pin: true`，并且同样适用于 `layout: page` 的页面。
5. 如果使用了 `hexo-offline` 插件，建议卸载，3.0 版本默认开启了 pjax 服务。

<!-- endtimeline -->

<!-- timeline 2020-05-15 [2.6.3 -> 2.6.6](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.6) -->

不需要额外处理。

<!-- endtimeline -->

<!-- timeline 2020-04-20 [2.6.2 -> 2.6.3](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.3) -->

1. 全局搜索 `seotitle` 并替换为 `seo_title`。
2. group 组件的索引规则有变，使用 group 组件的文章内，`group: group_name` 对应的组件名必须是 `group_name`。
2. group 组件的列表名优先显示文章的 `short_title` 其次是 `title`。

<!-- endtimeline -->

{% endtimeline %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% timeline 时间轴样式,blue %}

<!-- timeline 2020-07-24 [2.6.6 -> 3.0](https://github.com/volantis-x/hexo-theme-volantis/releases) -->

1. 如果有 `hexo-lazyload-image` 插件，需要删除并重新安装最新版本，设置 `lazyload.isSPA: true`。
2. 2.x 版本的 css 和 js 不适用于 3.x 版本，如果使用了 `use_cdn: true` 则需要删除。
3. 2.x 版本的 fancybox 标签在 3.x 版本中被重命名为 gallery 。
4. 2.x 版本的置顶 `top: true` 改为了 `pin: true`，并且同样适用于 `layout: page` 的页面。
5. 如果使用了 `hexo-offline` 插件，建议卸载，3.0 版本默认开启了 pjax 服务。

<!-- endtimeline -->

<!-- timeline 2020-05-15 [2.6.3 -> 2.6.6](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.6) -->

不需要额外处理。

<!-- endtimeline -->

<!-- timeline 2020-04-20 [2.6.2 -> 2.6.3](https://github.com/volantis-x/hexo-theme-volantis/releases/tag/2.6.3) -->

1. 全局搜索 `seotitle` 并替换为 `seo_title`。
2. group 组件的索引规则有变，使用 group 组件的文章内，`group: group_name` 对应的组件名必须是 `group_name`。
2. group 组件的列表名优先显示文章的 `short_title` 其次是 `title`。

<!-- endtimeline -->

{% endtimeline %}
```

<!-- endtab -->

{% endtabs %}

## 链接卡片 link

{% tabs link %}
<!-- tab 样式预览 -->

{% link 糖果屋教程贴, https://akilar.top/posts/615e2dec/, /img/siteicon/favicon.ico %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% link 糖果屋教程贴, https://akilar.top/posts/615e2dec/, /img/siteicon/favicon.ico %}
```

<!-- endtab -->

{% endtabs %}

## 按钮 btns

{% tabs btns %}
<!-- tab 样式预览 -->

1.如果需要显示类似「团队成员」之类的一组含有头像的链接：
{% btns circle grid5 %}
{% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
{% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
{% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
{% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
{% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
{% endbtns %}
2.或者含有图标的按钮：
{% btns rounded grid5 %}
{% cell 下载源码, /, fas fa-download %}
{% cell 查看文档, /, fas fa-book-open %}
{% endbtns %}
3.圆形图标 + 标题 + 描述 + 图片 + 网格5列 + 居中
{% btns circle center grid5 %}
<a href='https://apps.apple.com/cn/app/heart-mate-pro-hrm-utility/id1463348922?ls=1'>
  <i class='fab fa-apple'></i>
  <b>心率管家</b>
  {% p red, 专业版 %}
  <img src='https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/qrcode/heartmate_pro.png'>
</a>
<a href='https://apps.apple.com/cn/app/heart-mate-lite-hrm-utility/id1475747930?ls=1'>
  <i class='fab fa-apple'></i>
  <b>心率管家</b>
  {% p green, 免费版 %}
  <img src='https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/qrcode/heartmate_lite.png'>
</a>
{% endbtns %}

<!-- endtab -->

<!-- tab 源码 -->

1. 如果需要显示类似「团队成员」之类的一组含有头像的链接：

   ```
   MARKDOWN
   {% btns circle grid5 %}
   {% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
   {% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
   {% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
   {% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
   {% cell xaoxuu, https://xaoxuu.com, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png %}
   {% endbtns %}
   ```

2. 或者含有图标的按钮：

   ```
   MARKDOWN
   {% btns rounded grid5 %}
   {% cell 下载源码, /, fas fa-download %}
   {% cell 查看文档, /, fas fa-book-open %}
   {% endbtns %}
   ```

3. 圆形图标 + 标题 + 描述 + 图片 + 网格5列 + 居中

   ```
   MARKDOWN
   {% btns circle center grid5 %}
   <a href='https://apps.apple.com/cn/app/heart-mate-pro-hrm-utility/id1463348922?ls=1'>
     <i class='fab fa-apple'></i>
     <b>心率管家</b>
     {% p red, 专业版 %}
     <img src='https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/qrcode/heartmate_pro.png'>
   </a>
   <a href='https://apps.apple.com/cn/app/heart-mate-lite-hrm-utility/id1475747930?ls=1'>
     <i class='fab fa-apple'></i>
     <b>心率管家</b>
     {% p green, 免费版 %}
     <img src='https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/qrcode/heartmate_lite.png'>
   </a>
   {% endbtns %}
   ```

<!-- endtab -->

{% endtabs %}

## github卡片 ghcard

{% tabs ghcard %}
<!-- tab 样式预览 -->

1. 用户信息卡片

   
   MARKDOWN
   | {% ghcard xaoxuu %} | {% ghcard xaoxuu, theme=vue %} |
   | -- | -- |
   | {% ghcard xaoxuu, theme=buefy %} | {% ghcard xaoxuu, theme=solarized-light %} |
   | {% ghcard xaoxuu, theme=onedark %} | {% ghcard xaoxuu, theme=solarized-dark %} |
   | {% ghcard xaoxuu, theme=algolia %} | {% ghcard xaoxuu, theme=calm %} |
   
2. 仓库信息卡片

   
   MARKDOWN
   | {% ghcard volantis-x/hexo-theme-volantis %} | {% ghcard volantis-x/hexo-theme-volantis, theme=vue %} |
   | -- | -- |
   | {% ghcard volantis-x/hexo-theme-volantis, theme=buefy %} | {% ghcard volantis-x/hexo-theme-volantis, theme=solarized-light %} |
   | {% ghcard volantis-x/hexo-theme-volantis, theme=onedark %} | {% ghcard volantis-x/hexo-theme-volantis, theme=solarized-dark %} |
   | {% ghcard volantis-x/hexo-theme-volantis, theme=algolia %} | {% ghcard volantis-x/hexo-theme-volantis, theme=calm %} |
   

<!-- endtab -->

<!-- tab 源码 -->

1. 用户信息卡片

   ```
   MARKDOWN
   | {% ghcard xaoxuu %} | {% ghcard xaoxuu, theme=vue %} |
   | -- | -- |
   | {% ghcard xaoxuu, theme=buefy %} | {% ghcard xaoxuu, theme=solarized-light %} |
   | {% ghcard xaoxuu, theme=onedark %} | {% ghcard xaoxuu, theme=solarized-dark %} |
   | {% ghcard xaoxuu, theme=algolia %} | {% ghcard xaoxuu, theme=calm %} |
   ```

2. 仓库信息卡片

   ```
   MARKDOWN
   | {% ghcard volantis-x/hexo-theme-volantis %} | {% ghcard volantis-x/hexo-theme-volantis, theme=vue %} |
   | -- | -- |
   | {% ghcard volantis-x/hexo-theme-volantis, theme=buefy %} | {% ghcard volantis-x/hexo-theme-volantis, theme=solarized-light %} |
   | {% ghcard volantis-x/hexo-theme-volantis, theme=onedark %} | {% ghcard volantis-x/hexo-theme-volantis, theme=solarized-dark %} |
   | {% ghcard volantis-x/hexo-theme-volantis, theme=algolia %} | {% ghcard volantis-x/hexo-theme-volantis, theme=calm %} |
   ```

<!-- endtab -->

{% endtabs %}

## github徽标 ghbdage

{% tabs lik %}
<!-- tab 样式预览 -->

1.基本参数,定义徽标左右文字和图标
{% bdage Theme,Butterfly %}
{% bdage Frame,Hexo,hexo %}
2.信息参数，定义徽标右侧内容背景色，指向链接
{% bdage CDN,JsDelivr,jsDelivr||abcdef,https://metroui.org.ua/index.html,本站使用JsDelivr为静态资源提供CDN加速 %}
//如果是跨顺序省略可选参数，仍然需要写个逗号,用作分割
{% bdage Source,GitHub,GitHub||,https://github.com/ %}
3.拓展参数，支持shields的API的全部参数内容
{% bdage Hosted,Vercel,Vercel||brightgreen,https://vercel.com/,本站采用双线部署，默认线路托管于Vercel||style=social&logoWidth=20 %}
//如果是跨顺序省略可选参数组，仍然需要写双竖线||用作分割
{% bdage Hosted,Vercel,Vercel||||style=social&logoWidth=20&logoColor=violet %}

<!-- endtab -->

<!-- tab 源码 -->

1. 基本参数,定义徽标左右文字和图标

   ```
   MARKDOWN
   {% bdage Theme,Butterfly %}
   {% bdage Frame,Hexo,hexo %}
   ```

2. 信息参数，定义徽标右侧内容背景色，指向链接

   ```
   MARKDOWN
   {% bdage CDN,JsDelivr,jsDelivr||abcdef,https://metroui.org.ua/index.html,本站使用JsDelivr为静态资源提供CDN加速 %}
   //如果是跨顺序省略可选参数，仍然需要写个逗号,用作分割
   {% bdage Source,GitHub,GitHub||,https://github.com/ %}
   ```

3. 拓展参数，支持shields的API的全部参数内容

   ```
   MARKDOWN
   {% bdage Hosted,Vercel,Vercel||brightgreen,https://vercel.com/,本站采用双线部署，默认线路托管于Vercel||style=social&logoWidth=20 %}
   //如果是跨顺序省略可选参数组，仍然需要写双竖线||用作分割
   {% bdage Hosted,Vercel,Vercel||||style=social&logoWidth=20&logoColor=violet %}
   ```

<!-- endtab -->

{% endtabs %}

## 网站卡片 sites

{% tabs siek %}
<!-- tab 样式预览 -->

{% sitegroup %}
{% site xaoxuu, url=https://xaoxuu.com, screenshot=https://i.loli.net/2020/08/21/VuSwWZ1xAeUHEBC.jpg, avatar=https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png, description=简约风格 %}
{% site inkss, url=https://inkss.cn, screenshot=https://i.loli.net/2020/08/21/Vzbu3i8fXs6Nh5Y.jpg, avatar=https://cdn.jsdelivr.net/gh/inkss/common@master/static/web/avatar.jpg, description=这是一段关于这个网站的描述文字 %}
{% site MHuiG, url=https://blog.mhuig.top, screenshot=https://i.loli.net/2020/08/22/d24zpPlhLYWX6D1.png, avatar=https://cdn.jsdelivr.net/gh/MHuiG/imgbed@master/data/p.png, description=这是一段关于这个网站的描述文字 %}
{% site Colsrch, url=https://colsrch.top, screenshot=https://i.loli.net/2020/08/22/dFRWXm52OVu8qfK.png, avatar=https://cdn.jsdelivr.net/gh/Colsrch/images/Colsrch/avatar.jpg, description=这是一段关于这个网站的描述文字 %}
{% site Linhk1606, url=https://linhk1606.github.io, screenshot=https://i.loli.net/2020/08/21/3PmGLCKicnfow1x.png, avatar=https://i.loli.net/2020/02/09/PN7I5RJfFtA93r2.png, description=这是一段关于这个网站的描述文字 %}
{% endsitegroup %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% sitegroup %}
{% site xaoxuu, url=https://xaoxuu.com, screenshot=https://i.loli.net/2020/08/21/VuSwWZ1xAeUHEBC.jpg, avatar=https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets/avatar/avatar.png, description=简约风格 %}
{% site inkss, url=https://inkss.cn, screenshot=https://i.loli.net/2020/08/21/Vzbu3i8fXs6Nh5Y.jpg, avatar=https://cdn.jsdelivr.net/gh/inkss/common@master/static/web/avatar.jpg, description=这是一段关于这个网站的描述文字 %}
{% site MHuiG, url=https://blog.mhuig.top, screenshot=https://i.loli.net/2020/08/22/d24zpPlhLYWX6D1.png, avatar=https://cdn.jsdelivr.net/gh/MHuiG/imgbed@master/data/p.png, description=这是一段关于这个网站的描述文字 %}
{% site Colsrch, url=https://colsrch.top, screenshot=https://i.loli.net/2020/08/22/dFRWXm52OVu8qfK.png, avatar=https://cdn.jsdelivr.net/gh/Colsrch/images/Colsrch/avatar.jpg, description=这是一段关于这个网站的描述文字 %}
{% site Linhk1606, url=https://linhk1606.github.io, screenshot=https://i.loli.net/2020/08/21/3PmGLCKicnfow1x.png, avatar=https://i.loli.net/2020/02/09/PN7I5RJfFtA93r2.png, description=这是一段关于这个网站的描述文字 %}
{% endsitegroup %}
```

<!-- endtab -->

{% endtabs %}

## 行内图片 inlineimage

{% tabs link1 %}
<!-- tab 样式预览 -->

这是 {% inlineimage https://cdn.jsdelivr.net/gh/volantis-x/cdn-emoji/aru-l/0000.gif %} 一段话。

这又是 {% inlineimage https://cdn.jsdelivr.net/gh/volantis-x/cdn-emoji/aru-l/5150.gif, height=40px %} 一段话。

<!-- endtab -->

<!-- tab 源码 -->

```
这是 {% inlineimage https://cdn.jsdelivr.net/gh/volantis-x/cdn-emoji/aru-l/0000.gif %} 一段话。

这又是 {% inlineimage https://cdn.jsdelivr.net/gh/volantis-x/cdn-emoji/aru-l/5150.gif, height=40px %} 一段话。
```

<!-- endtab -->

{% endtabs %}

## 单张图片 image

{% tabs link2 %}
<!-- tab 样式预览 -->

1.添加描述：

{% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, alt=每天下课回宿舍的路，没有什么故事。 %}
2.指定宽度：
{% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, width=400px %}
3.指定宽度并添加描述：
{% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, width=400px, alt=每天下课回宿舍的路，没有什么故事。 %}
4.设置占位背景色：
{% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, wiidth=400px, bg=#1D0C04, alt=优化不同宽度浏览的观感 %}

<!-- endtab -->

<!-- tab 源码 -->

1. 添加描述：

   ```
   MARKDOWN
   {% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, alt=每天下课回宿舍的路，没有什么故事。 %}
   ```

2. 指定宽度：

   ```
   MARKDOWN
   {% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, width=400px %}
   ```

3. 指定宽度并添加描述：

   ```
   MARKDOWN
   {% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, width=400px, alt=每天下课回宿舍的路，没有什么故事。 %}
   ```

4. 设置占位背景色：

   ```
   MARKDOWN
   {% image https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/025.jpg, wiidth=400px, bg=#1D0C04, alt=优化不同宽度浏览的观感 %}
   ```

<!-- endtab -->

{% endtabs %}

## 音频 audio

{% tabs link3 %}
<!-- tab 样式预览 -->

{% audio https://github.com/volantis-x/volantis-docs/releases/download/assets/Lumia1020.mp3 %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% audio https://github.com/volantis-x/volantis-docs/releases/download/assets/Lumia1020.mp3 %}
```

<!-- endtab -->

{% endtabs %}

## 视频 video

{% tabs video %}
<!-- tab 样式预览 -->

100%宽度

{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
50%宽度

{% videos, 2 %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% endvideos %}
25%宽度

{% videos, 4 %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
{% endvideos %}

<!-- endtab -->

<!-- tab 源码 -->

1. 100%宽度

   ```
   MARKDOWN
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   ```

2. 50%宽度

   ```
   MARKDOWN
   {% videos, 2 %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% endvideos %}
   ```

3. 25%宽度

   ```
   MARKDOWN
   {% videos, 4 %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% video https://github.com/volantis-x/volantis-docs/releases/download/assets/IMG_0341.mov %}
   {% endvideos %}
   ```

<!-- endtab -->

{% endtabs %}

## 相册 gallery

{% tabs link3 %}
<!-- tab 样式预览 -->

gallerygroup 相册图库

<div class="gallery-group-main">
{% galleryGroup MC 在Rikkaの六花服务器里留下的足迹 '/gallery/MC/' https://npm.elemecdn.com/akilar-candyassets/image/1.jpg %}
{% galleryGroup Gundam 哦咧哇gundam哒！ '/gallery/Gundam/' https://npm.elemecdn.com/akilar-candyassets/image/20200907110508327.png %}
{% galleryGroup I-am-Akilar 某种意义上也算自拍吧 '/gallery/I-am-Akilar/' https://npm.elemecdn.com/akilar-candyassets/image/20200907113116651.png %}
</div>

gallery 相册

{% gallery %}
![](https://i.loli.net/2019/12/25/Fze9jchtnyJXMHN.jpg)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/ryLVePaqkYm4TEK.jpg)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/gEy5Zc1Ai6VuO4N.jpg)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/d6QHbytlSYO4FBG.jpg)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/6nepIJ1xTgufatZ.jpg)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/E7Jvr4eIPwUNmzq.jpg)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/mh19anwBSWIkGlH.jpg)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2tu9JC8ewpBFagv.jpg)
{% endgallery %}

<!-- endtab -->

<!-- tab 源码 -->

{% tip %}

对于很多同学提问的`gallerygroup`和`gallery`相册页的链接问题。这里说下我个人的使用习惯。
一般使用相册图库的话，可以在导航栏加一个gallery的page(**使用指令`hexo new page gallery`添加**)，里面放相册图库作为封面。然后在`[Blogroot]/source/gallery/`下面建立相应的文件夹，例如若按照这里的示例，若欲使用`/gallery/MC/`路径访问MC相册，则需要新建`[Blogroot]/source/gallery/MC/index.md`，并在里面填入`gallery`相册内容。

{% endtip %}

1. gallerygroup 相册图库

   ```
   MARKDOWN
   <div class="gallery-group-main">
   {% galleryGroup MC 在Rikkaの六花服务器里留下的足迹 '/gallery/MC/' https://npm.elemecdn.com/akilar-candyassets/image/1.jpg %}
   {% galleryGroup Gundam 哦咧哇gundam哒！ '/gallery/Gundam/' https://npm.elemecdn.com/akilar-candyassets/image/20200907110508327.png %}
   {% galleryGroup I-am-Akilar 某种意义上也算自拍吧 '/gallery/I-am-Akilar/' https://npm.elemecdn.com/akilar-candyassets/image/20200907113116651.png %}
   </div>
   ```

2. gallery 相册

   ```
   MARKDOWN
   {% gallery %}
   ![](https://i.loli.net/2019/12/25/Fze9jchtnyJXMHN.jpg)
   ![](https://i.loli.net/2019/12/25/ryLVePaqkYm4TEK.jpg)
   ![](https://i.loli.net/2019/12/25/gEy5Zc1Ai6VuO4N.jpg)
   ![](https://i.loli.net/2019/12/25/d6QHbytlSYO4FBG.jpg)
   ![](https://i.loli.net/2019/12/25/6nepIJ1xTgufatZ.jpg)
   ![](https://i.loli.net/2019/12/25/E7Jvr4eIPwUNmzq.jpg)
   ![](https://i.loli.net/2019/12/25/mh19anwBSWIkGlH.jpg)
   ![](https://i.loli.net/2019/12/25/2tu9JC8ewpBFagv.jpg)
   {% endgallery %}
   ```

<!-- endtab -->

{% endtabs %}

## 折叠框 folding

{% tabs folding %}
<!-- tab 样式预览 -->

{% folding 查看图片测试 %}

![](https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper/abstract/41F215B9-261F-48B4-80B5-4E86E165259E.jpeg)

{% endfolding %}

{% folding cyan open, 查看默认打开的折叠框 %}

这是一个默认打开的折叠框。

{% endfolding %}

{% folding green, 查看代码测试 %}
假装这里有代码块（代码块没法嵌套代码块）
{% endfolding %}

{% folding yellow, 查看列表测试 %}

- haha
- hehe

{% endfolding %}

{% folding red, 查看嵌套测试 %}

{% folding blue, 查看嵌套测试2 %}

{% folding 查看嵌套测试3 %}

hahaha <span><img src='https://cdn.jsdelivr.net/gh/volantis-x/cdn-emoji/tieba/滑稽.png' style='height:24px'></span>

{% endfolding %}

{% endfolding %}

{% endfolding %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% folding 查看图片测试 %}

![](https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper/abstract/41F215B9-261F-48B4-80B5-4E86E165259E.jpeg)

{% endfolding %}

{% folding cyan open, 查看默认打开的折叠框 %}

这是一个默认打开的折叠框。

{% endfolding %}

{% folding green, 查看代码测试 %}
假装这里有代码块（代码块没法嵌套代码块）
{% endfolding %}

{% folding yellow, 查看列表测试 %}

- haha
- hehe

{% endfolding %}

{% folding red, 查看嵌套测试 %}

{% folding blue, 查看嵌套测试2 %}

{% folding 查看嵌套测试3 %}

hahaha <span><img src='https://cdn.jsdelivr.net/gh/volantis-x/cdn-emoji/tieba/%E6%BB%91%E7%A8%BD.png' style='height:24px'></span>

{% endfolding %}

{% endfolding %}

{% endfolding %}
```

<!-- endtab -->

{% endtabs %}

## 诗词标签 poem

{% tabs link3 %}
<!-- tab 样式预览 -->

{% poem 水调歌头,苏轼 %}
丙辰中秋，欢饮达旦，大醉，作此篇，兼怀子由。
明月几时有？把酒问青天。
不知天上宫阙，今夕是何年？
我欲乘风归去，又恐琼楼玉宇，高处不胜寒。
起舞弄清影，何似在人间？

转朱阁，低绮户，照无眠。
不应有恨，何事长向别时圆？
人有悲欢离合，月有阴晴圆缺，此事古难全。
但愿人长久，千里共婵娟。
{% endpoem %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% poem 水调歌头,苏轼 %}
丙辰中秋，欢饮达旦，大醉，作此篇，兼怀子由。
明月几时有？把酒问青天。
不知天上宫阙，今夕是何年？
我欲乘风归去，又恐琼楼玉宇，高处不胜寒。
起舞弄清影，何似在人间？

转朱阁，低绮户，照无眠。
不应有恨，何事长向别时圆？
人有悲欢离合，月有阴晴圆缺，此事古难全。
但愿人长久，千里共婵娟。
{% endpoem %}
```

<!-- endtab -->

{% endtabs %}

## 阿里图标 icon

{% tabs icon %}
<!-- tab 样式预览 -->

{% icon icon-rat_zi %}{% icon icon-rat,2 %}

{% icon icon-ox_chou,3 %}{% icon icon-ox,4 %}

{% icon icon-tiger_yin,5 %}{% icon icon-tiger,6 %}

{% icon icon-rabbit_mao,1 %}{% icon icon-rabbit,2 %}

{% icon icon-dragon_chen,3 %}{% icon icon-dragon,4 %}

{% icon icon-snake_si,5 %}{% icon icon-snake,6 %}

{% icon icon-horse_wu %}{% icon icon-horse,2 %}

{% icon icon-goat_wei,3 %}{% icon icon-goat,4 %}

{% icon icon-monkey_shen,5 %}{% icon icon-monkey,6 %}

{% icon icon-rooster_you %}{% icon icon-rooster,2 %}

{% icon icon-dog_xu,3 %}{% icon icon-dog,4 %}

{% icon icon-boar_hai,5 %}{% icon icon-boar,6 %}

<!-- endtab -->

<!-- tab 源码 -->

{% tip %}本标签的图标需要自己额外引入阿里矢量图标库的样式，具体引入方案请移步：[Hexo引入阿里矢量图标库](https://akilar.top/posts/d2ebecef/){% endtip %}

```
{% icon icon-rat_zi %}{% icon icon-rat,2 %}

{% icon icon-ox_chou,3 %}{% icon icon-ox,4 %}

{% icon icon-tiger_yin,5 %}{% icon icon-tiger,6 %}

{% icon icon-rabbit_mao,1 %}{% icon icon-rabbit,2 %}

{% icon icon-dragon_chen,3 %}{% icon icon-dragon,4 %}

{% icon icon-snake_si,5 %}{% icon icon-snake,6 %}

{% icon icon-horse_wu %}{% icon icon-horse,2 %}

{% icon icon-goat_wei,3 %}{% icon icon-goat,4 %}

{% icon icon-monkey_shen,5 %}{% icon icon-monkey,6 %}

{% icon icon-rooster_you %}{% icon icon-rooster,2 %}

{% icon icon-dog_xu,3 %}{% icon icon-dog,4 %}

{% icon icon-boar_hai,5 %}{% icon icon-boar,6 %}
```

<!-- endtab -->

{% endtabs %}

## 特效标签wow

https://akilar.top/posts/abab51cf/

## 进度条 progress

{% tabs progress %}
<!-- tab 样式预览 -->

{% progress 10 red 进度条样式预览 %}
{% progress 30 yellow 进度条样式预览 %}
{% progress 50 green 进度条样式预览 %}
{% progress 70 cyan 进度条样式预览 %}
{% progress 90 blue 进度条样式预览 %}
{% progress 100 gray 进度条样式预览 %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% progress 10 red 进度条样式预览 %}
{% progress 30 yellow 进度条样式预览 %}
{% progress 50 green 进度条样式预览 %}
{% progress 70 cyan 进度条样式预览 %}
{% progress 90 blue 进度条样式预览 %}
{% progress 100 gray 进度条样式预览 %}
```

<!-- endtab -->

{% endtabs %}

## 气泡注释 bubble

{% tabs bubble %}
<!-- tab 样式预览 -->

最近我学到了不少新玩意儿（虽然对很多大佬来说这些已经是旧技术了），比如CSS的{% bubble 兄弟相邻选择器,"例如 h1 + p {margin-top:50px;}" %}，{% bubble flex布局,"Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性","#ec5830" %}，{% bubble transform变换,"transform 属性向元素应用 2D 或 3D 转换。该属性允许我们对元素进行旋转、缩放、移动或倾斜。","#1db675" %}，animation的{% bubble 贝塞尔速度曲线,"贝塞尔曲线(Bézier curve)，又称贝兹曲线或贝济埃曲线，是应用于二维图形应用程序的数学曲线。一般的矢量图形软件通过它来精确画出曲线，贝兹曲线由线段与节点组成，节点是可拖动的支点，线段像可伸缩的皮筋","#de4489" %}写法，还有今天刚看到的{% bubble clip-path,"clip-path属性使用裁剪方式创建元素的可显示区域。区域内的部分显示，区域外的隐藏。","#868fd7" %}属性。这些对我来说很新颖的概念狠狠的冲击着我以前积累起来的设计思路。

<!-- endtab -->

<!-- tab 源码 -->

```
最近我学到了不少新玩意儿（虽然对很多大佬来说这些已经是旧技术了），比如CSS的{% bubble 兄弟相邻选择器,"例如 h1 + p {margin-top:50px;}" %}，{% bubble flex布局,"Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性","#ec5830" %}，{% bubble transform变换,"transform 属性向元素应用 2D 或 3D 转换。该属性允许我们对元素进行旋转、缩放、移动或倾斜。","#1db675" %}，animation的{% bubble 贝塞尔速度曲线,"贝塞尔曲线(Bézier curve)，又称贝兹曲线或贝济埃曲线，是应用于二维图形应用程序的数学曲线。一般的矢量图形软件通过它来精确画出曲线，贝兹曲线由线段与节点组成，节点是可拖动的支点，线段像可伸缩的皮筋","#de4489" %}写法，还有今天刚看到的{% bubble clip-path,"clip-path属性使用裁剪方式创建元素的可显示区域。区域内的部分显示，区域外的隐藏。","#868fd7" %}属性。这些对我来说很新颖的概念狠狠的冲击着我以前积累起来的设计思路。
```

<!-- endtab -->

{% endtabs %}

## 引用文献 reference

{% tabs reference %}
<!-- tab 样式预览 -->

Akilarの糖果屋(akilar.top)是一个私人性质的博客{% referto '[1]','Akilarの糖果屋群聊简介' %}，从各类教程至生活点滴，无话不谈。建群的目的是提供一个闲聊的场所。博客采用Hexo框架{% referto '[2]','Hexo中文文档' %}，Butterfly主题{% referto '[3]','Butterfly 安装文档(一) 快速开始' %}

本项目参考了Volantis{% referto '[4]','hexo-theme-volantis 标签插件' %}的标签样式。引入`[tag].js`，并针对`butterfly`主题修改了相应的`[tag].styl`。在此鸣谢`Volantis`主题众开发者。
主要参考内容包括各个volantis的内置标签插件文档{% referto '[5]','Volantis文档:内置标签插件' %}
Butterfly主题的各个衍生魔改{% referto '[6]','Butterfly 安装文档:标签外挂（Tag Plugins' %}{% referto '[7]','小弋の生活馆全样式预览' %}{% referto '[8]','l-lin-font-awesome-animation' %}{% referto '[9]','小康的butterfly主题使用文档' %}



{% referfrom '[1]','Akilarの糖果屋群聊简介','https://jq.qq.com/?_wv=1027&k=pGLB2C0N' %}
{% referfrom '[2]','Hexo中文文档','https://hexo.io/zh-cn/docs/' %}
{% referfrom '[3]','Butterfly 安装文档(一) 快速开始','https://butterfly.js.org/posts/21cfbf15/' %}
{% referfrom '[4]','hexo-theme-volantis 标签插件','https://volantis.js.org/v5/tag-plugins/' %}
{% referfrom '[5]','Volantis文档:内置标签插件','https://volantis.js.org/tag-plugins/' %}
{% referfrom '[6]','Butterfly 安装文档:标签外挂（Tag Plugins','https://butterfly.js.org/posts/4aa8abbe/#%E6%A8%99%E7%B1%A4%E5%A4%96%E6%8E%9B%EF%BC%88Tag-Plugins%EF%BC%89' %}
{% referfrom '[7]','小弋の生活馆全样式预览','https://lovelijunyi.gitee.io/posts/c898.html' %}
{% referfrom '[8]','l-lin-font-awesome-animation','https://github.com/l-lin/font-awesome-animation' %}
{% referfrom '[9]','小康的butterfly主题使用文档','https://www.antmoe.com/posts/3b43914f/' %}

<!-- endtab -->

<!-- tab 源码 -->

```
Akilarの糖果屋(akilar.top)是一个私人性质的博客{% referto '[1]','Akilarの糖果屋群聊简介' %}，从各类教程至生活点滴，无话不谈。建群的目的是提供一个闲聊的场所。博客采用Hexo框架{% referto '[2]','Hexo中文文档' %}，Butterfly主题{% referto '[3]','Butterfly 安装文档(一) 快速开始' %}

本项目参考了Volantis{% referto '[4]','hexo-theme-volantis 标签插件' %}的标签样式。引入`[tag].js`，并针对`butterfly`主题修改了相应的`[tag].styl`。在此鸣谢`Volantis`主题众开发者。
主要参考内容包括各个volantis的内置标签插件文档{% referto '[5]','Volantis文档:内置标签插件' %}
Butterfly主题的各个衍生魔改{% referto '[6]','Butterfly 安装文档:标签外挂（Tag Plugins' %}{% referto '[7]','小弋の生活馆全样式预览' %}{% referto '[8]','l-lin-font-awesome-animation' %}{% referto '[9]','小康的butterfly主题使用文档' %}



{% referfrom '[1]','Akilarの糖果屋群聊简介','https://jq.qq.com/?_wv=1027&k=pGLB2C0N' %}
{% referfrom '[2]','Hexo中文文档','https://hexo.io/zh-cn/docs/' %}
{% referfrom '[3]','Butterfly 安装文档(一) 快速开始','https://butterfly.js.org/posts/21cfbf15/' %}
{% referfrom '[4]','hexo-theme-volantis 标签插件','https://volantis.js.org/v5/tag-plugins/' %}
{% referfrom '[5]','Volantis文档:内置标签插件','https://volantis.js.org/tag-plugins/' %}
{% referfrom '[6]','Butterfly 安装文档:标签外挂（Tag Plugins','https://butterfly.js.org/posts/4aa8abbe/#%E6%A8%99%E7%B1%A4%E5%A4%96%E6%8E%9B%EF%BC%88Tag-Plugins%EF%BC%89' %}
{% referfrom '[7]','小弋の生活馆全样式预览','https://lovelijunyi.gitee.io/posts/c898.html' %}
{% referfrom '[8]','l-lin-font-awesome-animation','https://github.com/l-lin/font-awesome-animation' %}
{% referfrom '[9]','小康的butterfly主题使用文档','https://www.antmoe.com/posts/3b43914f/' %}
```

<!-- endtab -->

{% endtabs %}

## 旋转相册 carousel

{% tabs carousel %}
<!-- tab 样式预览 -->

{% carousel 'SF','strike freedom' %}
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110444226.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110508327.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110525753.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110600751.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110621554.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110637459.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110654150.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110707916.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110719787.png)
![](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/20200907110731118.png)
{% endcarousel %}

<!-- endtab -->

<!-- tab 源码 -->

```
{% carousel 'SF','strike freedom' %}
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110444226.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110508327.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110525753.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110600751.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110621554.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110637459.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110654150.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110707916.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110719787.png)
![](https://npm.elemecdn.com/akilar-candyassets/image/20200907110731118.png)
{% endcarousel %}
```

<!-- endtab -->

{% endtabs %}
