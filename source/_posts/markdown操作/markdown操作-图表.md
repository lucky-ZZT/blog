---
title: markdown操作-图表
abbrlink: '96999800'
date: 2023-04-15 13:34:17
tags: markdown操作
swiper_index: 
category: markdown操作
keywords: markdown操作
cover:
highlight_shrink:
---
## 十一、流程图
https://github.com/mermaid-js/mermaid/blob/develop/README.zh-CN.md
### 1、横向流程图

> 代码:
>
> ````text
> ```mermaid
> graph LR
> A[方形]==>B(圆角)
> B==>C{条件a}
> C-->|a=1|D[结果1]
> C-->|a=2|E[结果2]
> F[横向流程图]
> ```
> ````

效果：

```
{% mermaid %} // hexo里的语法，typora不用加
graph LR
A[方形]==>B(圆角)
B==>C{条件a}
C-->|a=1|D[结果1]
C-->|a=2|E[结果2]
F[横向流程图]
{% endmermaid %}
```

{% mermaid %}
graph LR
A[方形]==>B(圆角)
B==>C{条件a}
C-->|a=1|D[结果1]
C-->|a=2|E[结果2]
F[横向流程图]
{% endmermaid %}



### 2、竖向流程图

> 代码:
> ````text
> ```mermaid //{% mermaid %}一样要加
>graph TD
>A[方形]==>B(圆角)
>B==>C{条件a}
>C-->|a=1|D[结果1]
>C-->|a=2|E[结果2]
>F[竖向流程图]
>```
>````

>效果:
{% mermaid %}
graph TD
A[方形]==>B(圆角)
B==>C{条件a}
C-->|a=1|D[结果1]
C-->|a=2|E[结果2]
F[竖向流程图]
{% endmermaid %}

### 3、时序图

>代码：
>
>```
>sequenceDiagram
>Alice->>John: Hello John, how are you?
>loop Healthcheck
>    John->>John: Fight against hypochondria
>end
>Note right of John: Rational thoughts!
>John-->>Alice: Great!
>John->>Bob: How about you?
>Bob-->>John: Jolly good!
>```

效果：
{% mermaid %}
sequenceDiagram
Alice->>John: Hello John, how are you?
loop Healthcheck
    John->>John: Fight against hypochondria
end
Note right of John: Rational thoughts!
John-->>Alice: Great!
John->>Bob: How about you?
Bob-->>John: Jolly good!
{% endmermaid %}




## 十二、表情符号

>代码:  //typora可用
>```text
>:happy:、:cry:、:man:
>```

>效果:
>:happy:、 :cry:、 :man:
