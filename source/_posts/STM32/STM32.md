---
title: STM32
category: STM32
abbrlink: b900f0d0
date: 2023-06-14 17:00:32
tags:
swiper_index:
keywords:
cover:
highlight_shrink:
---

转载自b站[江协科技](https://www.bilibili.com/video/BV1th411z7sn)

## 基础概述

### 外设表

| **英文缩写** | **名称**           | **英文缩写** | **名称**           |
| ------------ | ------------------ | ------------ | ------------------ |
| NVIC         | 嵌套向量中断控制器 | CAN          | CAN通信            |
| SysTick      | 系统滴答定时器     | USB          | USB通信            |
| RCC          | 复位和时钟控制     | RTC          | 实时时钟           |
| GPIO         | 通用IO口           | CRC          | CRC校验            |
| AFIO         | 复用IO口           | PWR          | 电源控制           |
| EXTI         | 外部中断           | BKP          | 备份寄存器         |
| TIM          | 定时器             | IWDG         | 独立看门狗         |
| ADC          | 模数转换器         | WWDG         | 窗口看门狗         |
| DMA          | 直接内存访问       | DAC          | 数模转换器         |
| USART        | 同步/异步串口通信  | SDIO         | SD卡接口           |
| I2C          | I2C通信            | FSMC         | 可变静态存储控制器 |
| SPI          | SPI通信            | USB OTG      | USB主机接口        |

### 命名规则

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230614170928254.png" alt="image-20230614170928254" style="zoom:67%;" />

### 系统结构

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230614171345362.png" alt="image-20230614171345362" style="zoom:67%;" />

### 引脚定义

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230614171643557.png" alt="image-20230614171643557" style="zoom:67%;" />

### 启动设置

![image-20230614172019165](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230614172019165.png)

### 最小结构

![image-20230614173442806](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230614173442806.png)

补充：使用32.768k的原因
$$
\begin{array}\\
2^{15} = 32768 \\
所以对该晶振进行15次二分频，就可以得到1hz的时钟
\end{array}
$$


## 软件安装

- keil （5及以上安装支持包）
- STLINK
- USB转插口

## 工程建立

基于库函数的开发方式

启动文件

- 启动文件

  E:\learning_materials\STM32入门教程资料\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\CMSIS\CM3\DeviceSupport\ST\STM32F10x\startup\arm

- 寄存器描述文件

  E:\learning_materials\STM32入门教程资料\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\CMSIS\CM3\DeviceSupport\ST\STM32F10x

- 内核寄存器描述

  E:\learning_materials\STM32入门教程资料\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\CMSIS\CM3\CoreSupport

  

- 添加头文件路径

![image-20230614214713055](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230614214713055.png)



- library添加

  E:\learning_materials\STM32入门教程资料\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\STM32F10x_StdPeriph_Driver
  
- 头包含，中断

  E:\learning_materials\STM32入门教程资料\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Project\STM32F10x_StdPeriph_Template

- 配置标准外设库

  ![image-20230615103844008](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230615103844008.png)



## GPIO

### 简介

- GPIO（General Purpose Input Output）通用输入输出口

- 可配置为8种输入输出模式引脚电平：0V~3.3V，部分引脚可容忍5V

- 输出模式下可控制端口输出高低电平，用以驱动LED、控制蜂鸣器、模拟通信协议输出时序等

- 输入模式下可读取端口的高低电平或电压，用于读取按键输入、外接模块电平信号输入、ADC电压采集、模拟通信协议接收数据等



基本结构

![image-20230615140134086](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230615140134086.png)

![image-20230619095209835](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619095209835.png)

模式

| **模式名称** | **性质** | **特征**                                           |
| ------------ | -------- | -------------------------------------------------- |
| 浮空输入     | 数字输入 | 可读取引脚电平，若引脚悬空，则电平不确定           |
| 上拉输入     | 数字输入 | 可读取引脚电平，内部连接上拉电阻，悬空时默认高电平 |
| 下拉输入     | 数字输入 | 可读取引脚电平，内部连接下拉电阻，悬空时默认低电平 |
| 模拟输入     | 模拟输入 | GPIO无效，引脚直接接入内部ADC                      |
| 开漏输出     | 数字输出 | 可输出引脚电平，高电平为高阻态，低电平接VSS        |
| 推挽输出     | 数字输出 | 可输出引脚电平，高电平接VDD，低电平接VSS           |
| 复用开漏输出 | 数字输出 | 由片上外设控制，高电平为高阻态，低电平接VSS        |
| 复用推挽输出 | 数字输出 | 由片上外设控制，高电平接VDD，低电平接VSS           |

### 输出

```c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"

int main(void)		//返回得是void类型，不然会报警告
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);	//打开GPIO的时钟
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
	
	GPIO_InitTypeDef GPIO_0;	// 初始化输入模式
	GPIO_0.GPIO_Mode = GPIO_Mode_Out_PP;	// 推挽输出（高低电平有效）
	GPIO_0.GPIO_Pin = GPIO_Pin_0;
	GPIO_0.GPIO_Speed = GPIO_Speed_50MHz;
	
	GPIO_InitTypeDef GPIO_1;
	GPIO_1.GPIO_Mode = GPIO_Mode_Out_OD;	// 开漏输出（低电平有效）
	GPIO_1.GPIO_Pin = GPIO_Pin_1;
	GPIO_1.GPIO_Speed = GPIO_Speed_50MHz;
	
	GPIO_InitTypeDef GPIO_13;
	GPIO_13.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_13.GPIO_Pin = GPIO_Pin_13;
	GPIO_13.GPIO_Speed = GPIO_Speed_50MHz;
	
	GPIO_InitTypeDef GPIO_All;
	GPIO_All.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_All.GPIO_Pin = GPIO_Pin_All;	// 	配置16个端口，也可以将每个端口‘与’起来（设置自己需要的端口）
	GPIO_All.GPIO_Speed = GPIO_Speed_50MHz;
	
	GPIO_Init(GPIOA, &GPIO_0);
	GPIO_Init(GPIOA, &GPIO_1);
	GPIO_Init(GPIOC, &GPIO_13);
	GPIO_Init(GPIOB, &GPIO_All);
	
	// GPIO_ResetBits(GPIOA, GPIO_Pin_0);
	GPIO_ResetBits(GPIOC, GPIO_Pin_13);

	while(1)
	{
		// 灯闪烁
		GPIO_SetBits(GPIOA, GPIO_Pin_0);	//GPIO的函数，复位和置位操作
		GPIO_WriteBit(GPIOA, GPIO_Pin_1, Bit_RESET); // 写入位	
		Delay_ms(500);
		GPIO_ResetBits(GPIOA, GPIO_Pin_0);
		GPIO_WriteBit(GPIOA, GPIO_Pin_1, Bit_SET);
		Delay_ms(500);
		
		// 流水灯
		//GPIO_Write(GPIOB, ~0x0008); // PA15,PB3,PB4这几个端口不能用，是调试端口，需要单独配置
		//Delay_ms(500);
		//GPIO_Write(GPIOB, ~0x0010);
		//Delay_ms(500);
		GPIO_Write(GPIOB, ~0x0020);
		Delay_ms(500);
		GPIO_Write(GPIOB, ~0x0040);
		Delay_ms(500);
		GPIO_Write(GPIOB, ~0x0080);
		Delay_ms(500);
		GPIO_Write(GPIOB, ~0x0100);
		Delay_ms(500);
	}
}
//	最后一行得是空行，不然会报警告

```

### 输入

- 数据类型

  | **关键字**         | **位数** | **表示范围**             | **stdint****关键字** | **ST****关键字** |
  | ------------------ | -------- | ------------------------ | -------------------- | ---------------- |
  | char               | 8        | -128 ~ 127               | int8_t               | s8               |
  | unsigned char      | 8        | 0 ~ 255                  | uint8_t              | u8               |
  | short              | 16       | -32768 ~ 32767           | int16_t              | s16              |
  | unsigned short     | 16       | 0 ~ 65535                | uint16_t             | u16              |
  | int                | 32       | -2147483648 ~ 2147483647 | int32_t              | s32              |
  | unsigned int       | 32       | 0 ~ 4294967295           | uint32_t             | u32              |
  | long               | 32       | -2147483648 ~ 2147483647 |                      |                  |
  | unsigned long      | 32       | 0 ~ 4294967295           |                      |                  |
  | long long          | 64       | -(2^64)/2 ~ (2^64)/2-1   | int64_t              |                  |
  | unsigned long long | 64       | 0 ~ (2^64)-1             | uint64_t             |                  |
  | float              | 32       | -3.4e38 ~ 3.4e38         |                      |                  |
  | double             | 64       | -1.7e308 ~ 1.7e308       |                      |                  |

- 封装程序

  头文件：(固定格式)

  ```c++
  #ifndef __LIGHT_SENSOR_H
  #define __LIGHT_SENSOR_H
  
  void LightSensor_Init(void);
  uint8_t LightSensor_Get(void);
  
  #endif
  
  ```

  输入（以光敏为例）

  ```c++
  #include "stm32f10x.h"                  // Device header
  
  void LightSensor_Init(void)
  {
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
  	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_13;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_Init(GPIOB, &GPIO_InitStructure);
  }
  
  uint8_t LightSensor_Get(void)
  {
  	return GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_13);   // 读取引脚输入（固定位）
  }
  
  ```

  

- 读取输出端口的用途

  ```c++
  void LED1_Turn(void) 	// 翻转
  {
  	if (GPIO_ReadOutputDataBit(GPIOA, GPIO_Pin_1) == 0)		//读取输出端口的用途
  	{
  		GPIO_SetBits(GPIOA, GPIO_Pin_1);
  	}
  	else
  	{
  		GPIO_ResetBits(GPIOA, GPIO_Pin_1);
  	}
  }
  
  ```

  

## 调试

### 可视化工具

本文使用OLED作为调试显示工具

| **函数**                              | **作用**             |
| ------------------------------------- | -------------------- |
| OLED_Init();                          | 初始化               |
| OLED_Clear();                         | 清屏                 |
| OLED_ShowChar(1, 1, 'A');             | 显示一个字符         |
| OLED_ShowString(1, 3, "HelloWorld!"); | 显示字符串           |
| OLED_ShowNum(2, 1, 12345, 5);         | 显示十进制数字       |
| OLED_ShowSignedNum(2, 7, -66, 2);     | 显示有符号十进制数字 |
| OLED_ShowHexNum(3, 1, 0xAA55, 4);     | 显示十六进制数字     |
| OLED_ShowBinNum(4, 1, 0xAA55, 16);    | 显示二进制数字       |



### keil调试模式

![image-20230619161044408](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619161044408.png)





## 中断系统

### 简介

- 68个可屏蔽中断通道，包含EXTI、TIM、ADC、USART、SPI、I2C、RTC等多个外设
- 使用NVIC统一管理中断，每个中断通道都拥有16个可编程的优先等级，可对优先级进行分组，进一步设置抢占优先级和响应优先级

### NVIC

- 结构

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619164515336.png" alt="image-20230619164515336" style="zoom:67%;" />



- 优先级分组

  NVIC的中断优先级由优先级寄存器的4位（0~15）决定，这4位可以进行切分，分为高n位的抢占优先级和低4-n位的响应优先级

  抢占优先级高的可以中断嵌套，响应优先级高的可以优先排队，抢占优先级和响应优先级均相同的按中断号排队

| **分组方式** | **抢占优先级**  | **响应优先级**  |
| ------------ | --------------- | --------------- |
| 分组0        | 0位，取值为0    | 4位，取值为0~15 |
| 分组1        | 1位，取值为0~1  | 3位，取值为0~7  |
| 分组2        | 2位，取值为0~3  | 2位，取值为0~3  |
| 分组3        | 3位，取值为0~7  | 1位，取值为0~1  |
| 分组4        | 4位，取值为0~15 | 0位，取值为0    |

### EXTI

EXTI（Extern Interrupt）外部中断

EXTI可以监测指定GPIO口的电平信号，当其指定的GPIO口产生电平变化时，EXTI将立即向NVIC发出中断申请，经过NVIC裁决后即可中断CPU主程序，使CPU执行EXTI对应的中断程序

支持的触发方式：上升沿/下降沿/双边沿/软件触发

支持的GPIO口：所有GPIO口，但相同的Pin不能同时触发中断通道数：16个GPIO_Pin，外加PVD输出、RTC闹钟、USB唤醒、以太网唤醒

触发响应方式：中断响应/事件响应

- 结构

  ![image-20230619164858028](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619164858028.png)

- 框架

  ![image-20230619164933871](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619164933871.png)

### 代码示例

```c++
#include "stm32f10x.h"                  // Device header

uint16_t CountSensor_Count;

void CountSensor_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);
	// EXTI,NVIC不需要开启时钟
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_14;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOB, &GPIO_InitStructure);
	
	GPIO_EXTILineConfig(GPIO_PortSourceGPIOB, GPIO_PinSource14);  // AFIO的函数，配置中断
	
	EXTI_InitTypeDef EXTI_InitStructure;
	EXTI_InitStructure.EXTI_Line = EXTI_Line14;
	EXTI_InitStructure.EXTI_LineCmd = ENABLE;
	EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;
	EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Falling;  //触发方式：上升沿，下降沿
	EXTI_Init(&EXTI_InitStructure);		//	配置外部中断
	
	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);	//	中断分组
	
	NVIC_InitTypeDef NVIC_InitStructure;
	NVIC_InitStructure.NVIC_IRQChannel = EXTI15_10_IRQn;
	NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
	NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 1;
	NVIC_InitStructure.NVIC_IRQChannelSubPriority = 1;
	NVIC_Init(&NVIC_InitStructure);		// 外部中断配置
}

uint16_t CountSensor_Get(void)
{
	return CountSensor_Count;
}

void EXTI15_10_IRQHandler(void)	//中断函数
{
	if (EXTI_GetITStatus(EXTI_Line14) == SET)
	{
		/*如果出现数据乱跳的现象，可再次判断引脚电平，以避免抖动*/
		if (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_14) == 0)
		{
			CountSensor_Count ++;
		}
		EXTI_ClearITPendingBit(EXTI_Line14);
	}
}

```

```c++
#include "stm32f10x.h"                  // Device header
#include "Delay.h"
#include "OLED.h"
#include "CountSensor.h"

int main(void)
{
	OLED_Init();
	CountSensor_Init();
	
	OLED_ShowString(1, 1, "Count:");
	
	while (1)
	{
		OLED_ShowNum(1, 7, CountSensor_Get(), 5);
	}
}

```



## 定时器

定时器可以对输入的时钟进行计数，并在计数值达到设定值时触发中断

16位计数器、预分频器、自动重装寄存器的时基单元，在72MHz计数时钟下可以实现最大59.65s的定时



### 类型

| **类型**   | **编号**               | **总线** | **功能**                                                     |
| ---------- | ---------------------- | -------- | ------------------------------------------------------------ |
| 高级定时器 | TIM1、TIM8             | APB2     | 拥有通用定时器全部功能，并额外具有重复计数器、死区生成、互补输出、刹车输入等功能 |
| 通用定时器 | TIM2、TIM3、TIM4、TIM5 | APB1     | 拥有基本定时器全部功能，并额外具有内外时钟源选择、输入捕获、输出比较、编码器接口、主从触发模式等功能 |
| 基本定时器 | TIM6、TIM7             | APB1     | 拥有定时中断、主模式触发DAC的功能                            |

STM32F103C8T6定时器资源：TIM1、TIM2、TIM3、TIM4

### 框架

![image-20230619200400541](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619200400541.png)

![image-20230625103451318](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230625103451318.png)



![image-20230625103505891](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230625103505891.png)

![image-20230619220433231](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619220433231.png)

### RCC时钟树

![image-20230625110214425](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230625110214425.png)

### 锁相环(PLL)

#### 功能：

使输出信号在频率和相位上能够与输入参考信号同步

#### 组成

![img](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/964cda49361943089ca8b1f370449709.png)

- PD鉴相器

  - 功能

    鉴别两个信号的相位差，并使用有效电平补偿该段误差

  - 原理

    简单的电路，可以是异或逻辑

    ![image-20230625122513224](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230625122513224.png)

    

- 环路滤波器(LF)
- 压控振荡器（VCO）



### 代码示例

- 内部时钟

  ```c++
  #include "stm32f10x.h"                  // Device header
  
  void Timer_Init(void)
  {
  	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
  	
  	TIM_InternalClockConfig(TIM2);	// 选择时钟（这里是内部时钟）
  	
  	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
  	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;		//分频
  	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;	//计数器模式
  	TIM_TimeBaseInitStructure.TIM_Period = 10000 - 1;	//计数（10k频的10000个分量周期就是1S）
  	TIM_TimeBaseInitStructure.TIM_Prescaler = 7200 - 1;	//分频（这里72M分频得到10k频）
  	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
  	TIM_TimeBaseInit(TIM2, &TIM_TimeBaseInitStructure);
  	
  	TIM_ClearFlag(TIM2, TIM_FLAG_Update);	//清除更新中断标志位,让计数从0开始
  	TIM_ITConfig(TIM2, TIM_IT_Update, ENABLE);	//使能中断
  	
  	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
  	
  	NVIC_InitTypeDef NVIC_InitStructure;
  	NVIC_InitStructure.NVIC_IRQChannel = TIM2_IRQn;
  	NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
  	NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 2;
  	NVIC_InitStructure.NVIC_IRQChannelSubPriority = 1;
  	NVIC_Init(&NVIC_InitStructure);
  	
  	TIM_Cmd(TIM2, ENABLE);	//启动定时器
  }
  
  /*
  void TIM2_IRQHandler(void)
  {
  	if (TIM_GetITStatus(TIM2, TIM_IT_Update) == SET)
  	{
  		
  		TIM_ClearITPendingBit(TIM2, TIM_IT_Update);
  	}
  }
  */
  
  ```

- 外部时钟

  ```c++
  #include "stm32f10x.h"                  // Device header
  
  void Timer_Init(void)
  {
  	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
  	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_Init(GPIOA, &GPIO_InitStructure);
  	
  	TIM_ETRClockMode2Config(TIM2, TIM_ExtTRGPSC_OFF, TIM_ExtTRGPolarity_NonInverted, 0x0F);
  	
  	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
  	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
  	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
  	TIM_TimeBaseInitStructure.TIM_Period = 10 - 1;
  	TIM_TimeBaseInitStructure.TIM_Prescaler = 1 - 1;
  	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
  	TIM_TimeBaseInit(TIM2, &TIM_TimeBaseInitStructure);
  	
  	TIM_ClearFlag(TIM2, TIM_FLAG_Update);
  	TIM_ITConfig(TIM2, TIM_IT_Update, ENABLE);
  	
  	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
  	
  	NVIC_InitTypeDef NVIC_InitStructure;
  	NVIC_InitStructure.NVIC_IRQChannel = TIM2_IRQn;
  	NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
  	NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 2;
  	NVIC_InitStructure.NVIC_IRQChannelSubPriority = 1;
  	NVIC_Init(&NVIC_InitStructure);
  	
  	TIM_Cmd(TIM2, ENABLE);
  }
  
  uint16_t Timer_GetCounter(void)
  {
  	return TIM_GetCounter(TIM2);
  }
  
  /*
  void TIM2_IRQHandler(void)
  {
  	if (TIM_GetITStatus(TIM2, TIM_IT_Update) == SET)
  	{
  		
  		TIM_ClearITPendingBit(TIM2, TIM_IT_Update);
  	}
  }
  */
  
  ```

  

### 输出比较OC

- 输出比较可以通过比较CNT与CCR寄存器值的关系，来对输出电平进行置1、置0或翻转的操作，用于输出一定频率和占空比的PWM波形

- PWM（Pulse Width Modulation）脉冲宽度调制在具有惯性的系统中，可以通过对一系列脉冲的宽度进行调制，来等效地获得所需要的模拟参量，常应用于电机控速等领域



#### 输出比较模式

| **模式**         |                           **描述**                           |
| ---------------- | :----------------------------------------------------------: |
| 冻结             |                  CNT=CCR时，REF保持为原状态                  |
| 匹配时置有效电平 |                   CNT=CCR时，REF置有效电平                   |
| 匹配时置无效电平 |                   CNT=CCR时，REF置无效电平                   |
| 匹配时电平翻转   |                    CNT=CCR时，REF电平翻转                    |
| 强制为无效电平   |               CNT与CCR无效，REF强制为无效电平                |
| 强制为有效电平   |               CNT与CCR无效，REF强制为有效电平                |
| PWM模式1         | 向上计数：CNT<CCR时，REF置有效电平，CNT≥CCR时，REF置无效电平。<br />向下计数：CNT>CCR时，REF置无效电平，CNT≤CCR时，REF置有效电平。 |
| PWM模式2         | 向上计数：CNT<CCR时，REF置无效电平，CNT≥CCR时，REF置有效电平。<br />向下计数：CNT>CCR时，REF置有效电平，CNT≤CCR时，REF置无效电平 |

![image-20230619224537861](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619224537861.png)

#### PWM

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619224837750.png" alt="image-20230619224837750" style="zoom:67%;" />

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230619224853388.png" alt="image-20230619224853388" style="zoom:67%;" />



#### 测试程序

```c++
#include "stm32f10x.h"                  // Device header

void PWM_Init(void)
{
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	
//	RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);
//	GPIO_PinRemapConfig(GPIO_PartialRemap1_TIM2, ENABLE);	//重映射
//	GPIO_PinRemapConfig(GPIO_Remap_SWJ_JTAGDisable, ENABLE);	//解除调试端口，解除JTAG复用
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP;	//选择复用推挽输出，将控制权给到TIM控制
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;		//GPIO_Pin_15;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	TIM_InternalClockConfig(TIM2);
	
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
	TIM_TimeBaseInitStructure.TIM_Period = 100 - 1;		//ARR
	TIM_TimeBaseInitStructure.TIM_Prescaler = 720 - 1;		//PSC
	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM2, &TIM_TimeBaseInitStructure);
	
	TIM_OCInitTypeDef TIM_OCInitStructure;
	TIM_OCStructInit(&TIM_OCInitStructure);		//给结构体变量赋初值
	TIM_OCInitStructure.TIM_OCMode = TIM_OCMode_PWM1;		//输出比较模式
	TIM_OCInitStructure.TIM_OCPolarity = TIM_OCPolarity_High;		//输出比较极性
	TIM_OCInitStructure.TIM_OutputState = TIM_OutputState_Enable;	//输出使能
	TIM_OCInitStructure.TIM_Pulse = 0;		//CCR
	TIM_OC1Init(TIM2, &TIM_OCInitStructure);
	
	TIM_Cmd(TIM2, ENABLE);	//启动定时器
}

void PWM_SetCompare1(uint16_t Compare)
{
	TIM_SetCompare1(TIM2, Compare);
}

void PWM_SetPrescaler(uint16_t Prescaler)
{
	TIM_PrescalerConfig(TIM2, Prescaler, TIM_PSCReloadMode_Immediate);
}

```

主函数

```c++
#include "stm32f10x.h"                  // Device header
#include "Delay.h"
#include "OLED.h"
#include "PWM.h"

uint8_t i;

int main(void)
{
	OLED_Init();
	PWM_Init();
	
	while (1)
	{
		for (i = 0; i <= 100; i++)	//变换占空比，变大
		{
			PWM_SetCompare1(i);
			Delay_ms(10);
		}
		for (i = 0; i <= 100; i++)	//占空比变小
		{
			PWM_SetCompare1(100 - i);
			Delay_ms(10);
		}
	}
}

```



### 输入捕获IC

- 输入捕获模式下，当通道输入引脚出现指定电平跳变时，当前CNT的值将被锁存到CCR中，可用于测量PWM波形的频率、占空比、脉冲间隔、电平持续时间等参数
- 每个高级定时器和通用定时器都拥有4个输入捕获通道
- 可配置为PWMI模式，同时测量频率和占空比
- 可配合主从触发模式，实现硬件全自动测量

#### 频率测量

![image-20230625214852205](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230625214852205.png)

- 测频法（适用于高频）：在闸门时间T内，对上升沿计次，得到N，则频率f_x=N / T
- 测周法（适用于低频）：两个上升沿内，以标准频率fc计次，得到N ，则频率f_x=f_c / N；（这里的标准频率是计次N的，从而算出一个周期的时间是N/f_c;频率是周期的导数）
- 中界频率：测频法与测周法误差相等的频率点f_m=√f_c / T

#### 输入通道捕获![image-20230626232323986](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230626232323986.png)



#### 主从触发模式

![image-20230626231501372](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230626231501372.png)

#### 输入捕获基本结构

![image-20230626232524139](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230626232524139.png)

#### PWMI基本结构(占空比)

![image-20230626232454957](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230626232454957.png)

#### 代码测试

- .c

```c++
#include "stm32f10x.h"                  // Device header

void IC_Init(void)
{
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM3, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_6;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	TIM_InternalClockConfig(TIM3);
	
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
	TIM_TimeBaseInitStructure.TIM_Period = 65536 - 1;		//ARR
	TIM_TimeBaseInitStructure.TIM_Prescaler = 72 - 1;		//PSC
	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM3, &TIM_TimeBaseInitStructure);
	
	TIM_ICInitTypeDef TIM_ICInitStructure;
	TIM_ICInitStructure.TIM_Channel = TIM_Channel_1;
	TIM_ICInitStructure.TIM_ICFilter = 0xF;
	TIM_ICInitStructure.TIM_ICPolarity = TIM_ICPolarity_Rising;
	TIM_ICInitStructure.TIM_ICPrescaler = TIM_ICPSC_DIV1;
	TIM_ICInitStructure.TIM_ICSelection = TIM_ICSelection_DirectTI;
	TIM_PWMIConfig(TIM3, &TIM_ICInitStructure);	//只支持通道1、2

	TIM_SelectInputTrigger(TIM3, TIM_TS_TI1FP1);
	TIM_SelectSlaveMode(TIM3, TIM_SlaveMode_Reset);
	
	TIM_Cmd(TIM3, ENABLE);
}

uint32_t IC_GetFreq(void)	//获取频率
{
	return 1000000 / (TIM_GetCapture1(TIM3) + 1);
}

uint32_t IC_GetDuty(void)	//获取占空比
{
	return (TIM_GetCapture2(TIM3) + 1) * 100 / (TIM_GetCapture1(TIM3) + 1);
}

```

- main

```c++
#include "stm32f10x.h"                  // Device header
#include "Delay.h"
#include "OLED.h"
#include "PWM.h"
#include "IC.h"

int main(void)
{
	OLED_Init();
	PWM_Init();
	IC_Init();
	
	OLED_ShowString(1, 1, "Freq:00000Hz");
	OLED_ShowString(2, 1, "Duty:00%");
	
	PWM_SetPrescaler(720 - 1);			//Freq = 72M / (PSC + 1) / 100
	PWM_SetCompare1(50);				//Duty = CCR / 100
	
	while (1)
	{
		OLED_ShowNum(1, 6, IC_GetFreq(), 5);
		OLED_ShowNum(2, 6, IC_GetDuty(), 2);
	}
}

```



## ADC

### 简介

- ADC（Analog-Digital Converter）模拟-数字转换器
- 输入电压范围：0~3.3V，转换结果范围：0~4095

### 逐次逼近型ADC

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629220455997.png" alt="image-20230629220455997" style="zoom:67%;" />

​	逐次逼近型adc由比较器、D/A转换器、缓冲寄存器和若干控制逻辑电路构成。原理是从高位到低位逐位比较，首先将缓冲寄存器各位清零；转换开始后，先将寄存器最高位置1，把值送入D/A转换器，经D/A转换后的模拟量送入比较器，称为 Vo，与比较器的待转换的模拟量Vi比较，若Vo<Vi，该位被保留，否则被清0。然后，再置寄存器次高位为1，将寄存器中新的数字量送D/A转换器，输出的 Vo再与Vi比较，若Vo<Vi，该位被保留，否则被清0。循环此过程，直到寄存器最低位，得到数字量的输出



### ADC框图

![image-20230629220718352](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629220718352.png)

### ADC基本结构

![image-20230629220740666](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629220740666.png)



### 输入通道

| **通道** | **ADC1**     | **ADC2** | **ADC3** |
| -------- | ------------ | -------- | -------- |
| 通道0    | PA0          | PA0      | PA0      |
| 通道1    | PA1          | PA1      | PA1      |
| 通道2    | PA2          | PA2      | PA2      |
| 通道3    | PA3          | PA3      | PA3      |
| 通道4    | PA4          | PA4      | PF6      |
| 通道5    | PA5          | PA5      | PF7      |
| 通道6    | PA6          | PA6      | PF8      |
| 通道7    | PA7          | PA7      | PF9      |
| 通道8    | PB0          | PB0      | PF10     |
| 通道9    | PB1          | PB1      |          |
| 通道10   | PC0          | PC0      | PC0      |
| 通道11   | PC1          | PC1      | PC1      |
| 通道12   | PC2          | PC2      | PC2      |
| 通道13   | PC3          | PC3      | PC3      |
| 通道14   | PC4          | PC4      |          |
| 通道15   | PC5          | PC5      |          |
| 通道16   | 温度传感器   |          |          |
| 通道17   | 内部参考电压 |          |          |



### 转换模式

- 连续转换，非扫描模式

  ![image-20230629220916730](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629220916730.png)

- 单次转换，非扫描模式

  ![image-20230629220943268](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629220943268.png)

- 连续转换，扫描模式

  ![image-20230629221905469](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629221905469.png)

- 单次转换，扫描模式

  ![image-20230629221801648](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629221801648.png)

  

### 触发控制

![image-20230629221941097](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629221941097.png)



### 数据对齐

![image-20230629222029798](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629222029798.png)



### 转换时间

- AD转换的步骤：采样，保持，量化，编码

- STM32 ADC的总转换时间为：
  $$
  T_{CONV} = 采样时间 + 12.5个ADC周期
  $$
  ​	

- 例如：当ADCCLK=14MHz，采样时间为1.5个ADC周期
  $$
  T_{CONV} = 1.5 + 12.5 = 14个ADC周期 = 1μs
  $$



### 校准

- ADC有一个内置自校准模式。校准可大幅减小因内部电容器组的变化而造成的准精度误差。校准期间，在每个电容器上都会计算出一个误差修正码(数字值)，这个码用于消除在随后的转换中每个电容器上产生的误差
- 建议在每次上电后执行一次校准
- 启动校准前， ADC必须处于关电状态超过至少两个ADC时钟周期



### 测试代码

```c++
#include "stm32f10x.h"                  // Device header

void AD_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_ADC1, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	
	RCC_ADCCLKConfig(RCC_PCLK2_Div6);	//72/6=12
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AIN;		//模拟输入，断开gpio
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	ADC_RegularChannelConfig(ADC1, ADC_Channel_0, 1, ADC_SampleTime_55Cycles5);
	
	ADC_InitTypeDef ADC_InitStructure;
	ADC_InitStructure.ADC_Mode = ADC_Mode_Independent;					//独立模式或双ADC模式
	ADC_InitStructure.ADC_DataAlign = ADC_DataAlign_Right;				//数据对齐
	ADC_InitStructure.ADC_ExternalTrigConv = ADC_ExternalTrigConv_None;	//触发源（软件触发）
	ADC_InitStructure.ADC_ContinuousConvMode = DISABLE;					//四种模式选择
	ADC_InitStructure.ADC_ScanConvMode = DISABLE;
	ADC_InitStructure.ADC_NbrOfChannel = 1;
	ADC_Init(ADC1, &ADC_InitStructure);
	
	ADC_Cmd(ADC1, ENABLE);
	
	ADC_ResetCalibration(ADC1);								//复位校准
	while (ADC_GetResetCalibrationStatus(ADC1) == SET);
	ADC_StartCalibration(ADC1);
	while (ADC_GetCalibrationStatus(ADC1) == SET);
}

uint16_t AD_GetValue(void)
{
	ADC_SoftwareStartConvCmd(ADC1, ENABLE);
	while (ADC_GetFlagStatus(ADC1, ADC_FLAG_EOC) == RESET);	//获取EOC标志位（软件或读取后自动清零（DR））
	return ADC_GetConversionValue(ADC1);		
}

```

多路转换实现方式1

```c++
#include "stm32f10x.h"                  // Device header

void AD_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_ADC1, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	
	RCC_ADCCLKConfig(RCC_PCLK2_Div6);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AIN;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
		
	ADC_InitTypeDef ADC_InitStructure;
	ADC_InitStructure.ADC_Mode = ADC_Mode_Independent;
	ADC_InitStructure.ADC_DataAlign = ADC_DataAlign_Right;
	ADC_InitStructure.ADC_ExternalTrigConv = ADC_ExternalTrigConv_None;
	ADC_InitStructure.ADC_ContinuousConvMode = DISABLE;
	ADC_InitStructure.ADC_ScanConvMode = DISABLE;
	ADC_InitStructure.ADC_NbrOfChannel = 1;
	ADC_Init(ADC1, &ADC_InitStructure);
	
	ADC_Cmd(ADC1, ENABLE);
	
	ADC_ResetCalibration(ADC1);
	while (ADC_GetResetCalibrationStatus(ADC1) == SET);
	ADC_StartCalibration(ADC1);
	while (ADC_GetCalibrationStatus(ADC1) == SET);
}

uint16_t AD_GetValue(uint8_t ADC_Channel)	//多通道实现方式1，直接改变菜单列表的第一个值
{
	ADC_RegularChannelConfig(ADC1, ADC_Channel, 1, ADC_SampleTime_55Cycles5);
	ADC_SoftwareStartConvCmd(ADC1, ENABLE);
	while (ADC_GetFlagStatus(ADC1, ADC_FLAG_EOC) == RESET);
	return ADC_GetConversionValue(ADC1);
}
```



## DMA

### 简介

- DMA（Direct Memory Access）直接存储器存取
- DMA可以提供外设和存储器或者存储器和存储器之间的高速数据传输，无须CPU干预，节省了CPU的资源
- 12个独立可配置的通道： DMA1（7个通道）， DMA2（5个通道）每个通道都支持软件触发和特定的硬件触发
- STM32F103C8T6 DMA资源：DMA1（7个通道）



### 存储器映像

| **类型**    | **起始地址**   | **存储器**                       | **用途**                  |
| ----------- | -------------- | -------------------------------- | ------------------------- |
| ROM         | 0x0800 0000    | 程序存储器Flash                  | 存储C语言编译后的程序代码 |
| 0x1FFF F000 | 系统存储器     | 存储BootLoader，用于串口下载     |                           |
| 0x1FFF F800 | 选项字节       | 存储一些独立于程序代码的配置参数 |                           |
| RAM         | 0x2000 0000    | 运行内存SRAM                     | 存储运行过程中的临时变量  |
| 0x4000 0000 | 外设寄存器     | 存储各个外设的配置参数           |                           |
| 0xE000 0000 | 内核外设寄存器 | 存储内核各个外设的配置参数       |                           |



### DMA框图

![image-20230629224843401](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629224843401.png)



### 基本结构

![image-20230629224904008](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629224904008.png)



![image-20230629224924636](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629224924636.png)





### 数据运转

<img src="https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629225009301.png" alt="image-20230629225009301" style="zoom:67%;" />



```c++
#include "stm32f10x.h"                  // Device header

uint16_t MyDMA_Size;

void MyDMA_Init(uint32_t AddrA, uint32_t AddrB, uint16_t Size)
{
	MyDMA_Size = Size;
	
	RCC_AHBPeriphClockCmd(RCC_AHBPeriph_DMA1, ENABLE);
	
	DMA_InitTypeDef DMA_InitStructure;
	DMA_InitStructure.DMA_PeripheralBaseAddr = AddrA;
	DMA_InitStructure.DMA_PeripheralDataSize = DMA_PeripheralDataSize_Byte;
	DMA_InitStructure.DMA_PeripheralInc = DMA_PeripheralInc_Enable;
	DMA_InitStructure.DMA_MemoryBaseAddr = AddrB;
	DMA_InitStructure.DMA_MemoryDataSize = DMA_MemoryDataSize_Byte;
	DMA_InitStructure.DMA_MemoryInc = DMA_MemoryInc_Enable;
	DMA_InitStructure.DMA_DIR = DMA_DIR_PeripheralSRC;
	DMA_InitStructure.DMA_BufferSize = Size;
	DMA_InitStructure.DMA_Mode = DMA_Mode_Normal;
	DMA_InitStructure.DMA_M2M = DMA_M2M_Enable;
	DMA_InitStructure.DMA_Priority = DMA_Priority_Medium;
	DMA_Init(DMA1_Channel1, &DMA_InitStructure);
	
	DMA_Cmd(DMA1_Channel1, DISABLE);
}

void MyDMA_Transfer(void)
{
	DMA_Cmd(DMA1_Channel1, DISABLE);
	DMA_SetCurrDataCounter(DMA1_Channel1, MyDMA_Size);
	DMA_Cmd(DMA1_Channel1, ENABLE);
	
	while (DMA_GetFlagStatus(DMA1_FLAG_TC1) == RESET);
	DMA_ClearFlag(DMA1_FLAG_TC1);
}

```



### ADC扫描模式

![image-20230629225423513](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/2023/image-20230629225423513.png)



```c++
#include "stm32f10x.h"                  // Device header

uint16_t AD_Value[4];

void AD_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_ADC1, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_AHBPeriphClockCmd(RCC_AHBPeriph_DMA1, ENABLE);
	
	RCC_ADCCLKConfig(RCC_PCLK2_Div6);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AIN;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	ADC_RegularChannelConfig(ADC1, ADC_Channel_0, 1, ADC_SampleTime_55Cycles5);
	ADC_RegularChannelConfig(ADC1, ADC_Channel_1, 2, ADC_SampleTime_55Cycles5);
	ADC_RegularChannelConfig(ADC1, ADC_Channel_2, 3, ADC_SampleTime_55Cycles5);
	ADC_RegularChannelConfig(ADC1, ADC_Channel_3, 4, ADC_SampleTime_55Cycles5);
		
	ADC_InitTypeDef ADC_InitStructure;
	ADC_InitStructure.ADC_Mode = ADC_Mode_Independent;
	ADC_InitStructure.ADC_DataAlign = ADC_DataAlign_Right;
	ADC_InitStructure.ADC_ExternalTrigConv = ADC_ExternalTrigConv_None;
	ADC_InitStructure.ADC_ContinuousConvMode = ENABLE;
	ADC_InitStructure.ADC_ScanConvMode = ENABLE;
	ADC_InitStructure.ADC_NbrOfChannel = 4;
	ADC_Init(ADC1, &ADC_InitStructure);
	
	DMA_InitTypeDef DMA_InitStructure;
	DMA_InitStructure.DMA_PeripheralBaseAddr = (uint32_t)&ADC1->DR;
	DMA_InitStructure.DMA_PeripheralDataSize = DMA_PeripheralDataSize_HalfWord;
	DMA_InitStructure.DMA_PeripheralInc = DMA_PeripheralInc_Disable;
	DMA_InitStructure.DMA_MemoryBaseAddr = (uint32_t)AD_Value;
	DMA_InitStructure.DMA_MemoryDataSize = DMA_MemoryDataSize_HalfWord;
	DMA_InitStructure.DMA_MemoryInc = DMA_MemoryInc_Enable;
	DMA_InitStructure.DMA_DIR = DMA_DIR_PeripheralSRC;
	DMA_InitStructure.DMA_BufferSize = 4;
	DMA_InitStructure.DMA_Mode = DMA_Mode_Circular;
	DMA_InitStructure.DMA_M2M = DMA_M2M_Disable;
	DMA_InitStructure.DMA_Priority = DMA_Priority_Medium;
	DMA_Init(DMA1_Channel1, &DMA_InitStructure);
	
	DMA_Cmd(DMA1_Channel1, ENABLE);
	ADC_DMACmd(ADC1, ENABLE);
	ADC_Cmd(ADC1, ENABLE);
	
	ADC_ResetCalibration(ADC1);
	while (ADC_GetResetCalibrationStatus(ADC1) == SET);
	ADC_StartCalibration(ADC1);
	while (ADC_GetCalibrationStatus(ADC1) == SET);
	
	ADC_SoftwareStartConvCmd(ADC1, ENABLE);
}

```









## 附录

### 各种小的模块程序

#### 延时

- .c文件

```c++
#include "stm32f10x.h"

/**
  * @brief  微秒级延时
  * @param  xus 延时时长，范围：0~233015
  * @retval 无
  */
void Delay_us(uint32_t xus)
{
	SysTick->LOAD = 72 * xus;				//设置定时器重装值
	SysTick->VAL = 0x00;					//清空当前计数值
	SysTick->CTRL = 0x00000005;				//设置时钟源为HCLK，启动定时器
	while(!(SysTick->CTRL & 0x00010000));	//等待计数到0
	SysTick->CTRL = 0x00000004;				//关闭定时器
}

/**
  * @brief  毫秒级延时
  * @param  xms 延时时长，范围：0~4294967295
  * @retval 无
  */
void Delay_ms(uint32_t xms)
{
	while(xms--)
	{
		Delay_us(1000);
	}
}
 
/**
  * @brief  秒级延时
  * @param  xs 延时时长，范围：0~4294967295
  * @retval 无
  */
void Delay_s(uint32_t xs)
{
	while(xs--)
	{
		Delay_ms(1000);
	}
} 

```

- .h

  ```c++
  #ifndef __DELAY_H
  #define __DELAY_H
  
  void Delay_us(uint32_t us);
  void Delay_ms(uint32_t ms);
  void Delay_s(uint32_t s);
  
  #endif
  
  ```

  

#### LED灯

- .c

  ```c++
  #include "stm32f10x.h"                  // Device header
  
  void LED_Init(void)
  {
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
  	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_2;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_Init(GPIOA, &GPIO_InitStructure);
  	
  	GPIO_SetBits(GPIOA, GPIO_Pin_1 | GPIO_Pin_2);
  }
  
  void LED1_ON(void)
  {
  	GPIO_ResetBits(GPIOA, GPIO_Pin_1);
  }
  
  void LED1_OFF(void)
  {
  	GPIO_SetBits(GPIOA, GPIO_Pin_1);
  }
  
  void LED1_Turn(void)
  {
  	if (GPIO_ReadOutputDataBit(GPIOA, GPIO_Pin_1) == 0)
  	{
  		GPIO_SetBits(GPIOA, GPIO_Pin_1);
  	}
  	else
  	{
  		GPIO_ResetBits(GPIOA, GPIO_Pin_1);
  	}
  }
  
  void LED2_ON(void)
  {
  	GPIO_ResetBits(GPIOA, GPIO_Pin_2);
  }
  
  void LED2_OFF(void)
  {
  	GPIO_SetBits(GPIOA, GPIO_Pin_2);
  }
  
  void LED2_Turn(void)
  {
  	if (GPIO_ReadOutputDataBit(GPIOA, GPIO_Pin_2) == 0)
  	{
  		GPIO_SetBits(GPIOA, GPIO_Pin_2);
  	}
  	else
  	{
  		GPIO_ResetBits(GPIOA, GPIO_Pin_2);
  	}
  }
  
  ```

- .h

  ```c++
  #ifndef __LED_H
  #define __LED_H
  
  void LED_Init(void);
  void LED1_ON(void);
  void LED1_OFF(void);
  void LED1_Turn(void);
  void LED2_ON(void);
  void LED2_OFF(void);
  void LED2_Turn(void);
  
  #endif
  
  ```

  

#### 按钮

- .c

  ```c++
   #include "stm32f10x.h"                  // Device header
  #include "Delay.h"
  
  void Key_Init(void)
  {
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
  	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_11;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_Init(GPIOB, &GPIO_InitStructure);
  }
  
  uint8_t Key_GetNum(void)
  {
  	uint8_t KeyNum = 0;
  	if (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_1) == 0)
  	{
  		Delay_ms(20);	// 消除抖动
  		while (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_1) == 0);  //等待松手
  		Delay_ms(20);	// 消除抖动
  		KeyNum = 1;
  	}
  	if (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_11) == 0)
  	{
  		Delay_ms(20);
  		while (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_11) == 0);
  		Delay_ms(20);
  		KeyNum = 2;
  	}
  	
  	return KeyNum;
  }
  
  ```

- .h

  ```c++
  #ifndef __KEY_H
  #define __KEY_H
  
  void Key_Init(void);
  uint8_t Key_GetNum(void);
  
  #endif
  
  ```

#### 蜂鸣器（3孔）

- .c

  ```c++
  #include "stm32f10x.h"                  // Device header
  
  void Buzzer_Init(void)
  {
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
  	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_12;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_Init(GPIOB, &GPIO_InitStructure);
  	
  	GPIO_SetBits(GPIOB, GPIO_Pin_12);
  }
  
  void Buzzer_ON(void)
  {
  	GPIO_ResetBits(GPIOB, GPIO_Pin_12);
  }
  
  void Buzzer_OFF(void)
  {
  	GPIO_SetBits(GPIOB, GPIO_Pin_12);
  }
  
  void Buzzer_Turn(void)
  {
  	if (GPIO_ReadOutputDataBit(GPIOB, GPIO_Pin_12) == 0)
  	{
  		GPIO_SetBits(GPIOB, GPIO_Pin_12);
  	}
  	else
  	{
  		GPIO_ResetBits(GPIOB, GPIO_Pin_12);
  	}
  }
  
  ```

- .h

  ```c++
  #ifndef __BUZZER_H
  #define __BUZZER_H
  
  void Buzzer_Init(void);
  void Buzzer_ON(void);
  void Buzzer_OFF(void);
  void Buzzer_Turn(void);
  
  #endif
  
  ```

  

#### 光敏（4孔）

- .c

  ```c++
  #include "stm32f10x.h"                  // Device header
  
  void LightSensor_Init(void)
  {
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
  	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_13;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_Init(GPIOB, &GPIO_InitStructure);
  }
  
  uint8_t LightSensor_Get(void)
  {
  	return GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_13);   // 读取引脚输入（固定位）
  }
  
  ```

- .h

  ```c++
  #ifndef __LIGHT_SENSOR_H
  #define __LIGHT_SENSOR_H
  
  void LightSensor_Init(void);
  uint8_t LightSensor_Get(void);
  
  #endif
  
  ```

#### OLED(4孔)

- .c

  ```c++
  #include "stm32f10x.h"
  #include "OLED_Font.h"
  
  /*引脚配置*/
  #define OLED_W_SCL(x)		GPIO_WriteBit(GPIOB, GPIO_Pin_8, (BitAction)(x))
  #define OLED_W_SDA(x)		GPIO_WriteBit(GPIOB, GPIO_Pin_9, (BitAction)(x))
  
  /*引脚初始化*/
  void OLED_I2C_Init(void)
  {
      RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
   	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_OD;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_8;
   	GPIO_Init(GPIOB, &GPIO_InitStructure);
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_9;
   	GPIO_Init(GPIOB, &GPIO_InitStructure);
  	
  	OLED_W_SCL(1);
  	OLED_W_SDA(1);
  }
  
  /**
    * @brief  I2C开始
    * @param  无
    * @retval 无
    */
  void OLED_I2C_Start(void)
  {
  	OLED_W_SDA(1);
  	OLED_W_SCL(1);
  	OLED_W_SDA(0);
  	OLED_W_SCL(0);
  }
  
  /**
    * @brief  I2C停止
    * @param  无
    * @retval 无
    */
  void OLED_I2C_Stop(void)
  {
  	OLED_W_SDA(0);
  	OLED_W_SCL(1);
  	OLED_W_SDA(1);
  }
  
  /**
    * @brief  I2C发送一个字节
    * @param  Byte 要发送的一个字节
    * @retval 无
    */
  void OLED_I2C_SendByte(uint8_t Byte)
  {
  	uint8_t i;
  	for (i = 0; i < 8; i++)
  	{
  		OLED_W_SDA(Byte & (0x80 >> i));
  		OLED_W_SCL(1);
  		OLED_W_SCL(0);
  	}
  	OLED_W_SCL(1);	//额外的一个时钟，不处理应答信号
  	OLED_W_SCL(0);
  }
  
  /**
    * @brief  OLED写命令
    * @param  Command 要写入的命令
    * @retval 无
    */
  void OLED_WriteCommand(uint8_t Command)
  {
  	OLED_I2C_Start();
  	OLED_I2C_SendByte(0x78);		//从机地址
  	OLED_I2C_SendByte(0x00);		//写命令
  	OLED_I2C_SendByte(Command); 
  	OLED_I2C_Stop();
  }
  
  /**
    * @brief  OLED写数据
    * @param  Data 要写入的数据
    * @retval 无
    */
  void OLED_WriteData(uint8_t Data)
  {
  	OLED_I2C_Start();
  	OLED_I2C_SendByte(0x78);		//从机地址
  	OLED_I2C_SendByte(0x40);		//写数据
  	OLED_I2C_SendByte(Data);
  	OLED_I2C_Stop();
  }
  
  /**
    * @brief  OLED设置光标位置
    * @param  Y 以左上角为原点，向下方向的坐标，范围：0~7
    * @param  X 以左上角为原点，向右方向的坐标，范围：0~127
    * @retval 无
    */
  void OLED_SetCursor(uint8_t Y, uint8_t X)
  {
  	OLED_WriteCommand(0xB0 | Y);					//设置Y位置
  	OLED_WriteCommand(0x10 | ((X & 0xF0) >> 4));	//设置X位置高4位
  	OLED_WriteCommand(0x00 | (X & 0x0F));			//设置X位置低4位
  }
  
  /**
    * @brief  OLED清屏
    * @param  无
    * @retval 无
    */
  void OLED_Clear(void)
  {  
  	uint8_t i, j;
  	for (j = 0; j < 8; j++)
  	{
  		OLED_SetCursor(j, 0);
  		for(i = 0; i < 128; i++)
  		{
  			OLED_WriteData(0x00);
  		}
  	}
  }
  
  /**
    * @brief  OLED显示一个字符
    * @param  Line 行位置，范围：1~4
    * @param  Column 列位置，范围：1~16
    * @param  Char 要显示的一个字符，范围：ASCII可见字符
    * @retval 无
    */
  void OLED_ShowChar(uint8_t Line, uint8_t Column, char Char)
  {      	
  	uint8_t i;
  	OLED_SetCursor((Line - 1) * 2, (Column - 1) * 8);		//设置光标位置在上半部分
  	for (i = 0; i < 8; i++)
  	{
  		OLED_WriteData(OLED_F8x16[Char - ' '][i]);			//显示上半部分内容
  	}
  	OLED_SetCursor((Line - 1) * 2 + 1, (Column - 1) * 8);	//设置光标位置在下半部分
  	for (i = 0; i < 8; i++)
  	{
  		OLED_WriteData(OLED_F8x16[Char - ' '][i + 8]);		//显示下半部分内容
  	}
  }
  
  /**
    * @brief  OLED显示字符串
    * @param  Line 起始行位置，范围：1~4
    * @param  Column 起始列位置，范围：1~16
    * @param  String 要显示的字符串，范围：ASCII可见字符
    * @retval 无
    */
  void OLED_ShowString(uint8_t Line, uint8_t Column, char *String)
  {
  	uint8_t i;
  	for (i = 0; String[i] != '\0'; i++)
  	{
  		OLED_ShowChar(Line, Column + i, String[i]);
  	}
  }
  
  /**
    * @brief  OLED次方函数
    * @retval 返回值等于X的Y次方
    */
  uint32_t OLED_Pow(uint32_t X, uint32_t Y)
  {
  	uint32_t Result = 1;
  	while (Y--)
  	{
  		Result *= X;
  	}
  	return Result;
  }
  
  /**
    * @brief  OLED显示数字（十进制，正数）
    * @param  Line 起始行位置，范围：1~4
    * @param  Column 起始列位置，范围：1~16
    * @param  Number 要显示的数字，范围：0~4294967295
    * @param  Length 要显示数字的长度，范围：1~10
    * @retval 无
    */
  void OLED_ShowNum(uint8_t Line, uint8_t Column, uint32_t Number, uint8_t Length)
  {
  	uint8_t i;
  	for (i = 0; i < Length; i++)							
  	{
  		OLED_ShowChar(Line, Column + i, Number / OLED_Pow(10, Length - i - 1) % 10 + '0');
  	}
  }
  
  /**
    * @brief  OLED显示数字（十进制，带符号数）
    * @param  Line 起始行位置，范围：1~4
    * @param  Column 起始列位置，范围：1~16
    * @param  Number 要显示的数字，范围：-2147483648~2147483647
    * @param  Length 要显示数字的长度，范围：1~10
    * @retval 无
    */
  void OLED_ShowSignedNum(uint8_t Line, uint8_t Column, int32_t Number, uint8_t Length)
  {
  	uint8_t i;
  	uint32_t Number1;
  	if (Number >= 0)
  	{
  		OLED_ShowChar(Line, Column, '+');
  		Number1 = Number;
  	}
  	else
  	{
  		OLED_ShowChar(Line, Column, '-');
  		Number1 = -Number;
  	}
  	for (i = 0; i < Length; i++)							
  	{
  		OLED_ShowChar(Line, Column + i + 1, Number1 / OLED_Pow(10, Length - i - 1) % 10 + '0');
  	}
  }
  
  /**
    * @brief  OLED显示数字（十六进制，正数）
    * @param  Line 起始行位置，范围：1~4
    * @param  Column 起始列位置，范围：1~16
    * @param  Number 要显示的数字，范围：0~0xFFFFFFFF
    * @param  Length 要显示数字的长度，范围：1~8
    * @retval 无
    */
  void OLED_ShowHexNum(uint8_t Line, uint8_t Column, uint32_t Number, uint8_t Length)
  {
  	uint8_t i, SingleNumber;
  	for (i = 0; i < Length; i++)							
  	{
  		SingleNumber = Number / OLED_Pow(16, Length - i - 1) % 16;
  		if (SingleNumber < 10)
  		{
  			OLED_ShowChar(Line, Column + i, SingleNumber + '0');
  		}
  		else
  		{
  			OLED_ShowChar(Line, Column + i, SingleNumber - 10 + 'A');
  		}
  	}
  }
  
  /**
    * @brief  OLED显示数字（二进制，正数）
    * @param  Line 起始行位置，范围：1~4
    * @param  Column 起始列位置，范围：1~16
    * @param  Number 要显示的数字，范围：0~1111 1111 1111 1111
    * @param  Length 要显示数字的长度，范围：1~16
    * @retval 无
    */
  void OLED_ShowBinNum(uint8_t Line, uint8_t Column, uint32_t Number, uint8_t Length)
  {
  	uint8_t i;
  	for (i = 0; i < Length; i++)							
  	{
  		OLED_ShowChar(Line, Column + i, Number / OLED_Pow(2, Length - i - 1) % 2 + '0');
  	}
  }
  
  /**
    * @brief  OLED初始化
    * @param  无
    * @retval 无
    */
  void OLED_Init(void)
  {
  	uint32_t i, j;
  	
  	for (i = 0; i < 1000; i++)			//上电延时
  	{
  		for (j = 0; j < 1000; j++);
  	}
  	
  	OLED_I2C_Init();			//端口初始化
  	
  	OLED_WriteCommand(0xAE);	//关闭显示
  	
  	OLED_WriteCommand(0xD5);	//设置显示时钟分频比/振荡器频率
  	OLED_WriteCommand(0x80);
  	
  	OLED_WriteCommand(0xA8);	//设置多路复用率
  	OLED_WriteCommand(0x3F);
  	
  	OLED_WriteCommand(0xD3);	//设置显示偏移
  	OLED_WriteCommand(0x00);
  	
  	OLED_WriteCommand(0x40);	//设置显示开始行
  	
  	OLED_WriteCommand(0xA1);	//设置左右方向，0xA1正常 0xA0左右反置
  	
  	OLED_WriteCommand(0xC8);	//设置上下方向，0xC8正常 0xC0上下反置
  
  	OLED_WriteCommand(0xDA);	//设置COM引脚硬件配置
  	OLED_WriteCommand(0x12);
  	
  	OLED_WriteCommand(0x81);	//设置对比度控制
  	OLED_WriteCommand(0xCF);
  
  	OLED_WriteCommand(0xD9);	//设置预充电周期
  	OLED_WriteCommand(0xF1);
  
  	OLED_WriteCommand(0xDB);	//设置VCOMH取消选择级别
  	OLED_WriteCommand(0x30);
  
  	OLED_WriteCommand(0xA4);	//设置整个显示打开/关闭
  
  	OLED_WriteCommand(0xA6);	//设置正常/倒转显示
  
  	OLED_WriteCommand(0x8D);	//设置充电泵
  	OLED_WriteCommand(0x14);
  
  	OLED_WriteCommand(0xAF);	//开启显示
  		
  	OLED_Clear();				//OLED清屏
  }
  
  ```

- .h

  ```c++
  #ifndef __OLED_H
  #define __OLED_H
  
  void OLED_Init(void);
  void OLED_Clear(void);
  void OLED_ShowChar(uint8_t Line, uint8_t Column, char Char);
  void OLED_ShowString(uint8_t Line, uint8_t Column, char *String);
  void OLED_ShowNum(uint8_t Line, uint8_t Column, uint32_t Number, uint8_t Length);
  void OLED_ShowSignedNum(uint8_t Line, uint8_t Column, int32_t Number, uint8_t Length);
  void OLED_ShowHexNum(uint8_t Line, uint8_t Column, uint32_t Number, uint8_t Length);
  void OLED_ShowBinNum(uint8_t Line, uint8_t Column, uint32_t Number, uint8_t Length);
  
  #endif
  
  ```

- font.h

  ```c++
  #ifndef __OLED_FONT_H
  #define __OLED_FONT_H
  
  /*OLED字模库，宽8像素，高16像素*/
  const uint8_t OLED_F8x16[][16]=
  {
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,//  0
  	
  	0x00,0x00,0x00,0xF8,0x00,0x00,0x00,0x00,
  	0x00,0x00,0x00,0x33,0x30,0x00,0x00,0x00,//! 1
  	
  	0x00,0x10,0x0C,0x06,0x10,0x0C,0x06,0x00,
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,//" 2
  	
  	0x40,0xC0,0x78,0x40,0xC0,0x78,0x40,0x00,
  	0x04,0x3F,0x04,0x04,0x3F,0x04,0x04,0x00,//# 3
  	
  	0x00,0x70,0x88,0xFC,0x08,0x30,0x00,0x00,
  	0x00,0x18,0x20,0xFF,0x21,0x1E,0x00,0x00,//$ 4
  	
  	0xF0,0x08,0xF0,0x00,0xE0,0x18,0x00,0x00,
  	0x00,0x21,0x1C,0x03,0x1E,0x21,0x1E,0x00,//% 5
  	
  	0x00,0xF0,0x08,0x88,0x70,0x00,0x00,0x00,
  	0x1E,0x21,0x23,0x24,0x19,0x27,0x21,0x10,//& 6
  	
  	0x10,0x16,0x0E,0x00,0x00,0x00,0x00,0x00,
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,//' 7
  	
  	0x00,0x00,0x00,0xE0,0x18,0x04,0x02,0x00,
  	0x00,0x00,0x00,0x07,0x18,0x20,0x40,0x00,//( 8
  	
  	0x00,0x02,0x04,0x18,0xE0,0x00,0x00,0x00,
  	0x00,0x40,0x20,0x18,0x07,0x00,0x00,0x00,//) 9
  	
  	0x40,0x40,0x80,0xF0,0x80,0x40,0x40,0x00,
  	0x02,0x02,0x01,0x0F,0x01,0x02,0x02,0x00,//* 10
  	
  	0x00,0x00,0x00,0xF0,0x00,0x00,0x00,0x00,
  	0x01,0x01,0x01,0x1F,0x01,0x01,0x01,0x00,//+ 11
  	
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
  	0x80,0xB0,0x70,0x00,0x00,0x00,0x00,0x00,//, 12
  	
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
  	0x00,0x01,0x01,0x01,0x01,0x01,0x01,0x01,//- 13
  	
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
  	0x00,0x30,0x30,0x00,0x00,0x00,0x00,0x00,//. 14
  	
  	0x00,0x00,0x00,0x00,0x80,0x60,0x18,0x04,
  	0x00,0x60,0x18,0x06,0x01,0x00,0x00,0x00,/// 15
  	
  	0x00,0xE0,0x10,0x08,0x08,0x10,0xE0,0x00,
  	0x00,0x0F,0x10,0x20,0x20,0x10,0x0F,0x00,//0 16
  	
  	0x00,0x10,0x10,0xF8,0x00,0x00,0x00,0x00,
  	0x00,0x20,0x20,0x3F,0x20,0x20,0x00,0x00,//1 17
  	
  	0x00,0x70,0x08,0x08,0x08,0x88,0x70,0x00,
  	0x00,0x30,0x28,0x24,0x22,0x21,0x30,0x00,//2 18
  	
  	0x00,0x30,0x08,0x88,0x88,0x48,0x30,0x00,
  	0x00,0x18,0x20,0x20,0x20,0x11,0x0E,0x00,//3 19
  	
  	0x00,0x00,0xC0,0x20,0x10,0xF8,0x00,0x00,
  	0x00,0x07,0x04,0x24,0x24,0x3F,0x24,0x00,//4 20
  	
  	0x00,0xF8,0x08,0x88,0x88,0x08,0x08,0x00,
  	0x00,0x19,0x21,0x20,0x20,0x11,0x0E,0x00,//5 21
  	
  	0x00,0xE0,0x10,0x88,0x88,0x18,0x00,0x00,
  	0x00,0x0F,0x11,0x20,0x20,0x11,0x0E,0x00,//6 22
  	
  	0x00,0x38,0x08,0x08,0xC8,0x38,0x08,0x00,
  	0x00,0x00,0x00,0x3F,0x00,0x00,0x00,0x00,//7 23
  	
  	0x00,0x70,0x88,0x08,0x08,0x88,0x70,0x00,
  	0x00,0x1C,0x22,0x21,0x21,0x22,0x1C,0x00,//8 24
  	
  	0x00,0xE0,0x10,0x08,0x08,0x10,0xE0,0x00,
  	0x00,0x00,0x31,0x22,0x22,0x11,0x0F,0x00,//9 25
  	
  	0x00,0x00,0x00,0xC0,0xC0,0x00,0x00,0x00,
  	0x00,0x00,0x00,0x30,0x30,0x00,0x00,0x00,//: 26
  	
  	0x00,0x00,0x00,0x80,0x00,0x00,0x00,0x00,
  	0x00,0x00,0x80,0x60,0x00,0x00,0x00,0x00,//; 27
  	
  	0x00,0x00,0x80,0x40,0x20,0x10,0x08,0x00,
  	0x00,0x01,0x02,0x04,0x08,0x10,0x20,0x00,//< 28
  	
  	0x40,0x40,0x40,0x40,0x40,0x40,0x40,0x00,
  	0x04,0x04,0x04,0x04,0x04,0x04,0x04,0x00,//= 29
  	
  	0x00,0x08,0x10,0x20,0x40,0x80,0x00,0x00,
  	0x00,0x20,0x10,0x08,0x04,0x02,0x01,0x00,//> 30
  	
  	0x00,0x70,0x48,0x08,0x08,0x08,0xF0,0x00,
  	0x00,0x00,0x00,0x30,0x36,0x01,0x00,0x00,//? 31
  	
  	0xC0,0x30,0xC8,0x28,0xE8,0x10,0xE0,0x00,
  	0x07,0x18,0x27,0x24,0x23,0x14,0x0B,0x00,//@ 32
  	
  	0x00,0x00,0xC0,0x38,0xE0,0x00,0x00,0x00,
  	0x20,0x3C,0x23,0x02,0x02,0x27,0x38,0x20,//A 33
  	
  	0x08,0xF8,0x88,0x88,0x88,0x70,0x00,0x00,
  	0x20,0x3F,0x20,0x20,0x20,0x11,0x0E,0x00,//B 34
  	
  	0xC0,0x30,0x08,0x08,0x08,0x08,0x38,0x00,
  	0x07,0x18,0x20,0x20,0x20,0x10,0x08,0x00,//C 35
  	
  	0x08,0xF8,0x08,0x08,0x08,0x10,0xE0,0x00,
  	0x20,0x3F,0x20,0x20,0x20,0x10,0x0F,0x00,//D 36
  	
  	0x08,0xF8,0x88,0x88,0xE8,0x08,0x10,0x00,
  	0x20,0x3F,0x20,0x20,0x23,0x20,0x18,0x00,//E 37
  	
  	0x08,0xF8,0x88,0x88,0xE8,0x08,0x10,0x00,
  	0x20,0x3F,0x20,0x00,0x03,0x00,0x00,0x00,//F 38
  	
  	0xC0,0x30,0x08,0x08,0x08,0x38,0x00,0x00,
  	0x07,0x18,0x20,0x20,0x22,0x1E,0x02,0x00,//G 39
  	
  	0x08,0xF8,0x08,0x00,0x00,0x08,0xF8,0x08,
  	0x20,0x3F,0x21,0x01,0x01,0x21,0x3F,0x20,//H 40
  	
  	0x00,0x08,0x08,0xF8,0x08,0x08,0x00,0x00,
  	0x00,0x20,0x20,0x3F,0x20,0x20,0x00,0x00,//I 41
  	
  	0x00,0x00,0x08,0x08,0xF8,0x08,0x08,0x00,
  	0xC0,0x80,0x80,0x80,0x7F,0x00,0x00,0x00,//J 42
  	
  	0x08,0xF8,0x88,0xC0,0x28,0x18,0x08,0x00,
  	0x20,0x3F,0x20,0x01,0x26,0x38,0x20,0x00,//K 43
  	
  	0x08,0xF8,0x08,0x00,0x00,0x00,0x00,0x00,
  	0x20,0x3F,0x20,0x20,0x20,0x20,0x30,0x00,//L 44
  	
  	0x08,0xF8,0xF8,0x00,0xF8,0xF8,0x08,0x00,
  	0x20,0x3F,0x00,0x3F,0x00,0x3F,0x20,0x00,//M 45
  	
  	0x08,0xF8,0x30,0xC0,0x00,0x08,0xF8,0x08,
  	0x20,0x3F,0x20,0x00,0x07,0x18,0x3F,0x00,//N 46
  	
  	0xE0,0x10,0x08,0x08,0x08,0x10,0xE0,0x00,
  	0x0F,0x10,0x20,0x20,0x20,0x10,0x0F,0x00,//O 47
  	
  	0x08,0xF8,0x08,0x08,0x08,0x08,0xF0,0x00,
  	0x20,0x3F,0x21,0x01,0x01,0x01,0x00,0x00,//P 48
  	
  	0xE0,0x10,0x08,0x08,0x08,0x10,0xE0,0x00,
  	0x0F,0x18,0x24,0x24,0x38,0x50,0x4F,0x00,//Q 49
  	
  	0x08,0xF8,0x88,0x88,0x88,0x88,0x70,0x00,
  	0x20,0x3F,0x20,0x00,0x03,0x0C,0x30,0x20,//R 50
  	
  	0x00,0x70,0x88,0x08,0x08,0x08,0x38,0x00,
  	0x00,0x38,0x20,0x21,0x21,0x22,0x1C,0x00,//S 51
  	
  	0x18,0x08,0x08,0xF8,0x08,0x08,0x18,0x00,
  	0x00,0x00,0x20,0x3F,0x20,0x00,0x00,0x00,//T 52
  	
  	0x08,0xF8,0x08,0x00,0x00,0x08,0xF8,0x08,
  	0x00,0x1F,0x20,0x20,0x20,0x20,0x1F,0x00,//U 53
  	
  	0x08,0x78,0x88,0x00,0x00,0xC8,0x38,0x08,
  	0x00,0x00,0x07,0x38,0x0E,0x01,0x00,0x00,//V 54
  	
  	0xF8,0x08,0x00,0xF8,0x00,0x08,0xF8,0x00,
  	0x03,0x3C,0x07,0x00,0x07,0x3C,0x03,0x00,//W 55
  	
  	0x08,0x18,0x68,0x80,0x80,0x68,0x18,0x08,
  	0x20,0x30,0x2C,0x03,0x03,0x2C,0x30,0x20,//X 56
  	
  	0x08,0x38,0xC8,0x00,0xC8,0x38,0x08,0x00,
  	0x00,0x00,0x20,0x3F,0x20,0x00,0x00,0x00,//Y 57
  	
  	0x10,0x08,0x08,0x08,0xC8,0x38,0x08,0x00,
  	0x20,0x38,0x26,0x21,0x20,0x20,0x18,0x00,//Z 58
  	
  	0x00,0x00,0x00,0xFE,0x02,0x02,0x02,0x00,
  	0x00,0x00,0x00,0x7F,0x40,0x40,0x40,0x00,//[ 59
  	
  	0x00,0x0C,0x30,0xC0,0x00,0x00,0x00,0x00,
  	0x00,0x00,0x00,0x01,0x06,0x38,0xC0,0x00,//\ 60
  	
  	0x00,0x02,0x02,0x02,0xFE,0x00,0x00,0x00,
  	0x00,0x40,0x40,0x40,0x7F,0x00,0x00,0x00,//] 61
  	
  	0x00,0x00,0x04,0x02,0x02,0x02,0x04,0x00,
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,//^ 62
  	
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
  	0x80,0x80,0x80,0x80,0x80,0x80,0x80,0x80,//_ 63
  	
  	0x00,0x02,0x02,0x04,0x00,0x00,0x00,0x00,
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,//` 64
  	
  	0x00,0x00,0x80,0x80,0x80,0x80,0x00,0x00,
  	0x00,0x19,0x24,0x22,0x22,0x22,0x3F,0x20,//a 65
  	
  	0x08,0xF8,0x00,0x80,0x80,0x00,0x00,0x00,
  	0x00,0x3F,0x11,0x20,0x20,0x11,0x0E,0x00,//b 66
  	
  	0x00,0x00,0x00,0x80,0x80,0x80,0x00,0x00,
  	0x00,0x0E,0x11,0x20,0x20,0x20,0x11,0x00,//c 67
  	
  	0x00,0x00,0x00,0x80,0x80,0x88,0xF8,0x00,
  	0x00,0x0E,0x11,0x20,0x20,0x10,0x3F,0x20,//d 68
  	
  	0x00,0x00,0x80,0x80,0x80,0x80,0x00,0x00,
  	0x00,0x1F,0x22,0x22,0x22,0x22,0x13,0x00,//e 69
  	
  	0x00,0x80,0x80,0xF0,0x88,0x88,0x88,0x18,
  	0x00,0x20,0x20,0x3F,0x20,0x20,0x00,0x00,//f 70
  	
  	0x00,0x00,0x80,0x80,0x80,0x80,0x80,0x00,
  	0x00,0x6B,0x94,0x94,0x94,0x93,0x60,0x00,//g 71
  	
  	0x08,0xF8,0x00,0x80,0x80,0x80,0x00,0x00,
  	0x20,0x3F,0x21,0x00,0x00,0x20,0x3F,0x20,//h 72
  	
  	0x00,0x80,0x98,0x98,0x00,0x00,0x00,0x00,
  	0x00,0x20,0x20,0x3F,0x20,0x20,0x00,0x00,//i 73
  	
  	0x00,0x00,0x00,0x80,0x98,0x98,0x00,0x00,
  	0x00,0xC0,0x80,0x80,0x80,0x7F,0x00,0x00,//j 74
  	
  	0x08,0xF8,0x00,0x00,0x80,0x80,0x80,0x00,
  	0x20,0x3F,0x24,0x02,0x2D,0x30,0x20,0x00,//k 75
  	
  	0x00,0x08,0x08,0xF8,0x00,0x00,0x00,0x00,
  	0x00,0x20,0x20,0x3F,0x20,0x20,0x00,0x00,//l 76
  	
  	0x80,0x80,0x80,0x80,0x80,0x80,0x80,0x00,
  	0x20,0x3F,0x20,0x00,0x3F,0x20,0x00,0x3F,//m 77
  	
  	0x80,0x80,0x00,0x80,0x80,0x80,0x00,0x00,
  	0x20,0x3F,0x21,0x00,0x00,0x20,0x3F,0x20,//n 78
  	
  	0x00,0x00,0x80,0x80,0x80,0x80,0x00,0x00,
  	0x00,0x1F,0x20,0x20,0x20,0x20,0x1F,0x00,//o 79
  	
  	0x80,0x80,0x00,0x80,0x80,0x00,0x00,0x00,
  	0x80,0xFF,0xA1,0x20,0x20,0x11,0x0E,0x00,//p 80
  	
  	0x00,0x00,0x00,0x80,0x80,0x80,0x80,0x00,
  	0x00,0x0E,0x11,0x20,0x20,0xA0,0xFF,0x80,//q 81
  	
  	0x80,0x80,0x80,0x00,0x80,0x80,0x80,0x00,
  	0x20,0x20,0x3F,0x21,0x20,0x00,0x01,0x00,//r 82
  	
  	0x00,0x00,0x80,0x80,0x80,0x80,0x80,0x00,
  	0x00,0x33,0x24,0x24,0x24,0x24,0x19,0x00,//s 83
  	
  	0x00,0x80,0x80,0xE0,0x80,0x80,0x00,0x00,
  	0x00,0x00,0x00,0x1F,0x20,0x20,0x00,0x00,//t 84
  	
  	0x80,0x80,0x00,0x00,0x00,0x80,0x80,0x00,
  	0x00,0x1F,0x20,0x20,0x20,0x10,0x3F,0x20,//u 85
  	
  	0x80,0x80,0x80,0x00,0x00,0x80,0x80,0x80,
  	0x00,0x01,0x0E,0x30,0x08,0x06,0x01,0x00,//v 86
  	
  	0x80,0x80,0x00,0x80,0x00,0x80,0x80,0x80,
  	0x0F,0x30,0x0C,0x03,0x0C,0x30,0x0F,0x00,//w 87
  	
  	0x00,0x80,0x80,0x00,0x80,0x80,0x80,0x00,
  	0x00,0x20,0x31,0x2E,0x0E,0x31,0x20,0x00,//x 88
  	
  	0x80,0x80,0x80,0x00,0x00,0x80,0x80,0x80,
  	0x80,0x81,0x8E,0x70,0x18,0x06,0x01,0x00,//y 89
  	
  	0x00,0x80,0x80,0x80,0x80,0x80,0x80,0x00,
  	0x00,0x21,0x30,0x2C,0x22,0x21,0x30,0x00,//z 90
  	
  	0x00,0x00,0x00,0x00,0x80,0x7C,0x02,0x02,
  	0x00,0x00,0x00,0x00,0x00,0x3F,0x40,0x40,//{ 91
  	
  	0x00,0x00,0x00,0x00,0xFF,0x00,0x00,0x00,
  	0x00,0x00,0x00,0x00,0xFF,0x00,0x00,0x00,//| 92
  	
  	0x00,0x02,0x02,0x7C,0x80,0x00,0x00,0x00,
  	0x00,0x40,0x40,0x3F,0x00,0x00,0x00,0x00,//} 93
  	
  	0x00,0x06,0x01,0x01,0x02,0x02,0x04,0x04,
  	0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,//~ 94
  };
  
  #endif
  
  ```

  

#### EXTI中断

- .c

  ```c++
  #include "stm32f10x.h"                  // Device header
  
  uint16_t CountSensor_Count;
  
  void CountSensor_Init(void)
  {
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
  	RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);
  	// EXTI,NVIC不需要开启时钟
  	
  	GPIO_InitTypeDef GPIO_InitStructure;
  	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
  	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_14;
  	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
  	GPIO_Init(GPIOB, &GPIO_InitStructure);
  	
  	GPIO_EXTILineConfig(GPIO_PortSourceGPIOB, GPIO_PinSource14);  // AFIO的函数，配置中断
  	
  	EXTI_InitTypeDef EXTI_InitStructure;
  	EXTI_InitStructure.EXTI_Line = EXTI_Line14;
  	EXTI_InitStructure.EXTI_LineCmd = ENABLE;
  	EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;
  	EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Falling;  //触发方式：上升沿，下降沿
  	EXTI_Init(&EXTI_InitStructure);		//	配置外部中断
  	
  	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);	//	中断分组
  	
  	NVIC_InitTypeDef NVIC_InitStructure;
  	NVIC_InitStructure.NVIC_IRQChannel = EXTI15_10_IRQn;
  	NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
  	NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 1;
  	NVIC_InitStructure.NVIC_IRQChannelSubPriority = 1;
  	NVIC_Init(&NVIC_InitStructure);		// 外部中断配置
  }
  
  uint16_t CountSensor_Get(void)
  {
  	return CountSensor_Count;
  }
  
  void EXTI15_10_IRQHandler(void)	//中断函数
  {
  	if (EXTI_GetITStatus(EXTI_Line14) == SET)
  	{
  		/*如果出现数据乱跳的现象，可再次判断引脚电平，以避免抖动*/
  		if (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_14) == 0)
  		{
  			CountSensor_Count ++;
  		}
  		EXTI_ClearITPendingBit(EXTI_Line14);
  	}
  }
  
  ```

  

- .h

  ```c++
  #ifndef __COUNT_SENSOR_H
  #define __COUNT_SENSOR_H
  
  void CountSensor_Init(void);
  uint16_t CountSensor_Get(void);
  
  #endif
  
  ```

  
