---
title: ad基础
category: PCB
abbrlink: 97834b19
date: 2023-05-30 11:08:44
tags:
swiper_index:
keywords:
cover:
highlight_shrink:
---

## AD工程组成和创建

(1)组成

- 原理图库
- 原理图
- PCB库
- PCB
- 生产文件



(2)创建

- 创建工程![image-20230530120701135](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230530120701135.png)

- 创建原理图库、原理图、PCB库、PCB

  ![image-20230530121615880](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230530121615880.png)



## 元件库创建

- 元件模型的组成

  边框、引脚（注意电气属性）、描述

- 操作界面

  基本操作

  ![Snipaste_2023-05-30_15-12-52](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/Snipaste_2023-05-30_15-12-52.png)

  

  描述

  - 其中，Designator（常见写法R?、U?、C？、J?等）

  ![Snipaste_2023-05-30_15-17-21](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/Snipaste_2023-05-30_15-17-21.png)

  

- 快捷键

  新建模型：TC

  对齐：	A

  移动;	M

  元件旋转:	space

  位号递增复制： 	shift拖动



- 其他

  排针可以使用阵列粘贴，粘贴多个引脚（编辑菜单下）
  
  

## 原理图绘制

- 放置元件

- 连线，编写网络标号

- 元件编号

  快捷键：TAA

  ![image-20230607125502356](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230607125502356.png)

- 封装

  工具——封装管理器

- 错误检测

  - 设置检查规则

    工程选项

    <img src="C:\Users\ZZT\AppData\Roaming\Typora\typora-user-images\image-20230703125105829.png" alt="image-20230703125105829" style="zoom:67%;" />

  
  
  ![image-20230607132010763](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230607132010763.png)
  
  - 编译
  
    <img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230703125236466.png" alt="image-20230703125236466" style="zoom:67%;" />
  
  



## PCB元件绘制

- 组成

  ![image-20230607133219290](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230607133219290.png)

  阻焊：防止绿油覆盖

  通孔，表贴

  测量：ctrl+m  删除测量数据shift + c

  顶部覆盖层：TOP Overlayer  

  画直线：PL

  按坐标移动：M

  设置原点：EOS

  将原点定位到中心点：EFC

  阵列粘贴：复制后EA

  改变线的角度：shift + 空格

  只显示当前层：shift + s

  捕捉层上的点：shift + e(可以切换所有层)

  翻转：VB

- IPC封装向导

  安装扩展

  ![image-20230607140823814](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230607140823814.png)

  ![image-20230607140959966](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230607140959966.png)

## PCB绘制

- 加载元件到PCB

  导入可能存在的问题：没有封装，管脚缺失，管脚号不匹配

- 消除绿色报错

  进入该界面

  ![image-20230607201015179](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230607201015179.png)

  关闭所以，再复位错误标志

  白线是圆环：短路（可能原因焊盘参数Jumper改为0）

- PCB中各层

  丝印层（书写文字）

  - top overlay
  - bottom overlay

  阻焊层（阻碍锡膏向外流）

  - top solder
  - bottom solder

  助焊层（钢网开孔，预留刷锡）

  - top paste
  - bottom paste

  机械层（注释，不显示（与丝印层的区别））

  - 板框，定位孔

  keep-outlayer

  - 划线的地方做切痕

- 布局
  - 工具——器件摆放——矩阵
  - 在机械层画边框（Q换单位，调节尺寸是用到）
  - 设置原点（EOS）
  - 重新定义板框（DSD）
  - 设计层数（DK），层叠管理器
  
- 设置快捷键

  按住ctrl，再选对应的操作即可

  常用快捷键

  |     拉线     |     过孔     |    覆铜    | 器件排列离散 |    线选    |    框选    |
  | :----------: | :----------: | :--------: | :----------: | :--------: | :--------: |
  |      F2      |      F3      |     F4     |   F6(TOL)    |     2      |     3      |
  |    左对齐    |    右对齐    |   上对齐   |    下对齐    | 水平等间距 | 垂直等间距 |
  |     Num4     |     Num6     |    Num8    |     Num2     |    Num7    |    Num9    |
  | 器件位号排列 |    差分线    |  删除网格  |   物理选择   |  执行DRC   |    规则    |
  |     Num5     |    Alt+F2    |   Alt+`    |    ctrl+h    |     TD     |     DR     |
  |    Class     | 网络显示关闭 |    移动    |     选择     |  单位切换  |  单层显示  |
  |      DC      |      N       |     M      |      S       |     Q      |  shift+s   |
  |   切换抓取   |   多跟走线   | 忽略障碍物 |              |            |            |
  |   shift+e    |     TTM      |  shift+r   |              |            |            |

- 布局

  - 在原理图中选中模块，在PCB中在使用TOL布局
  - 隐藏电源线（设置类DC，在类中添加电源线，隐藏）

- 连线

  - 设计规则

    间距规则：6mil成本最低

    线宽：信号线宽大于6mil，(信号10，电源10), 优先级

    过孔：12mil以上，盘（2*h正负2mil）,未应用成功时，在设置里更改

    焊盘：反焊盘（8mil），手工考虑十字连接，载流考虑全连接，回流焊全连接。过孔全连接

  - 打扇孔

    
