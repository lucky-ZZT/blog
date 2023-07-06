---
title: verilog
category: FPGA
abbrlink: ffaf1e77
date: 2023-05-29 10:52:36
tags:
swiper_index:
keywords:
cover:
highlight_shrink:
---



原文链接：https://blog.csdn.net/jac_chao/article/details/123744724

## 标识符

- 用途： 用于定义常数、变量、信号、端口、子模块或参数名称。
- 组成：字母、数字、$、下划线任意组合而成
- 注意事项：
  - 区分大小写
  - 第一个字符是字母或者下划线



## 逻辑值

- 0: 低电平
- 1：高电平
- x: 表示状态未知
- z：表示高阻状态

注意：Z,X不区分大小写。（例如0z1x和0Z1X表示同一个数据）



## 逻辑运算

(1) 逻辑运算符：&&(与)、==（相等）、||（或）、!=（不等）

- 如 m&&n : 判断m和n是否全为真(非0即为真)，真则输出1'b1，否则输出1'b0 (4’b1010&4’b0101 = 1’b1)
- 最后输出结果只有1bit

(2) 按位运算符： &、|、~、^、~&、~^、~| 

- 如 m&n : 是把m的每一位与n的每一位按位做与运算 (4’b1010&4’b0101 = 4’b0000)
- 输出结果与m/n的bit数相同

(3) 归约运算符： &、|、~、^、&、~^、~| 

- 只有一个参量参与运算时( &为一元运算符),表示规约与，即向量内部进行与运算

```verilog
&a [3：0] // AND:a[3]&a[2]&a[1]&a [0]相当于(a[3：0]== 4'hf)
|b [3：0] // OR: b[3]|b[2]|b[1]|b [0]相当于(b[3：0]!= 4'h0)
^c [2：0] // XOR:c[2]^c[1]^c[0]
```

- 即(&4’b0101 = 0&1&0&1 = 1'b0 )
- 最后输出结果只有1bit



## 常量

与C语言类似，常量主要有：整数型、实数型和字符串型三种

（1）整数

- 用十进制表示常量
  1. 直接写18表示位宽为32bit的十进制数18；
  2. -15表示十进制的-15，用二进制补码表示至少需要5bit，即1_0001，最高一位为符号位；如果用6bit表示，则为11_0001，同样最高一位为符号位。

- 用基数表示法表示（写法清晰，更推荐）

  基本格式

  ```
   [换算为二进制后位宽的总长度][’][数值进制符号][与数值进制符号对应的数值]
  ```

  1. 8’hab表示8bit的十六进制数，换算成二进制是1010_1011；
  2. 8’d171表示8bit的十进制数，换算成二进制是1010_1011；
  3. 8’o253表示8bit的八进制数，换算成二进制是1010_1011；
  4. 8’b1010_1011表示8bit的二进制数，二进制就是1010_1011。



注意事项：

- 当表示二进制时，最好每4位写一个下划线以增强可读性：如8'b1000_1100  与8'b10001100 是一样的
- 基数表示法中遇到x时：十六进制表示4个x，八进制中表示3个x 
- 当位宽大于二进制位数时左边自动补0，小于二进制数时2从左边截断！



(2) 字符串

- 每个字符由1个8位的ASCII码值表示，即需要1byte存储空间

- 如：“Hello world”  字符串由11个ASCII符号构成，需要11byte存储空间



## 变量

1. 线网型（wire）：表示电路间的物理连接；
2. 寄存器型(reg)：Verilog中一个抽象的数据存储单元

注意事项：

- 凡是在always或initial语句中被赋值的变量（赋值号左边的变量），不论表达的是组合逻辑还是时序逻辑，都一定是reg型变量；
- 凡是在assign语句中被赋值的变量，一定是wire型变量。



## 参数

和C的静态常量类似

(1) 参数是一种常量，通常出现在module内部，常被用于定义状态、数据位宽等

```
parameter STATE = 1'b0;
```

(2) 只作用于声明的那个文件，且可以被灵活改变！

(3) 局部参数localparam，只在本模块中使用

```
localparam  STATE= 1'b1’;
```

(4) 参数的名称一般为大写，以区分其他变量 



注意：

- 实例化时，参数可修改

```verilog
parameter IDLE = 3’b001;
parameter CNT_1S_WIDTH = 4’d15
Parameter CNT_MAX = 25’d24_999_999


counter
#(
.CNT_MAX (25’d24 ) //实例化时参数可修改
)
counter_inst
(
.sys_clk (sys_clk ), //input sys_clk
.sys_rst_n (sys_rst_n ), //input sys_rst_n
.led_out (led_out ) //output led_out
);
```





## 向量

vector(向量)，是一组信号的集合,可视为位宽超过1bit 的 wire 信号。

(1) 定义方式

```verilog
格式：input/output  wire/reg [upper:lower] vector_name
 
//输入输出型
input [7:0] a,b,
output reg [7:0] out
 
// 模块中间向量
wire [7:0] c, e;
reg [7:0] d;
```

- [upper:lower] 定义位宽，如 [7:0] 表示位宽为8 bit ，即upper=7，lower=0
- vector_name可以一次写多个向量



（2）向量片选

- a[3:0]  取向量a的0~4位数据
- b[n]   取向量b的第n位数据
- c[-1:-2] 取向量c的最低2位数据
- c[0:3]   取向量c的最高4位数据

多路选择器应用：实现一个 256 选 1 选择器，sel 信号作为选择信号，当 sel = 0 时选择 in[3:0]，sel = 1 时选择 in[7:4],以此类推。

```
module top_module (
	input [1023:0] in,
	input [7:0] sel,
	output [3:0] out
);
	assign out = {in[sel*4+3], in[sel*4+2], in[sel*4+1], in[sel*4+0]};
 
	// assign out = in[sel*4 +: 4];		
	// assign out = in[sel*4+3 -: 4];	
endmodule
```

- 片选信号sel输入为n位二进制数，当参与运算、充当索引时会自动转换成十进制数
- 该题所选取的信号片段为: in[sel*4+3: sel*4] ,但这不符合Verilog的片选语法规则故应写成：
  in[sel*4 +: 4]   表示索引从sel*4开始的高4bit信号
  in[sel*4+3 -: 4] 表示索引从sel*4+3开始的低4bit信号
- 或是直接选出需要的每一位，再用{ }拼接成新向量：
  {in[sel*4+3], in[sel*4+2], in[sel*4+1], in[sel*4+0]}

## 赋值语句

- 阻塞赋值

  ```verilog
  //阻塞赋值
  // 组合块
  always @(*)  begin
  	out1 = a ;
      a = b ;
      out2 = a ;
  end
  //组合always块中用阻塞式赋值
  //执行顺序：按照begin_end语句块中的顺序依次执行，上述输出结果为：out1 = a ，out2 = b
  ```

  

- 非阻塞赋值

  ```verilog
  //非阻塞赋值(<=)
  // 时序块
  always @(posedge clk)  begin
  	out1 <= a ;
      a <= b ;
      out2 <= a ;
  end
  //时序always块中用非阻塞赋值
  //执行顺序：begin_end中所有语句并行执行，上述输出结果为：out1 = a ，out2 = a
  ```

  

## 三目运算符

```
condition ? if_true : if_false
```

当条件为真，表达式值为if_true ，否则表达式值为if_false。

以选择器为例：

```verilog
assign  out = (sel == 1'b1) ? in1 : in2;
```



## 分支语句

- if

  ```verilog
  if(<条件表达式 1>)
      语句或语句块 1;
  else if(<条件表达式 2>)
      语句或语句块 2;
      ………
  else
      语句或语句块 n;
  ```

- case

  ```verilog
  case(<控制表达式>)
      <分支语句 1> : 语句块 1;
      <分支语句 2> : 语句块 2;
      <分支语句 3> : 语句块 3;
      ………
      <分支语句 n> : 语句块 n;
   
      default : 语句块 n+1;
  endcase
  ```

  

## for循环

```verilog
integer i;
always @(*)  begin 
    for(i=0; i<n; i++)  begin: for_name
        <循环语句>
    end
end
```



## 运算符

- 关系运算符

  \>、<、>=、<=

  - 运算结果为真返回 1
  - 运算结果为假返回 0
  - 若某个操作数值不定(x)，则返回值为 x

- 拼接运算符

  用一对花括号加逗号组成“{ , }”拼接运算符，逗号隔开的数据按顺序拼接成新数据！

  ```verilog
  wire [1:0] a;
  wire [3:0] b;
  wire [5:0] c;
  wire [11:0] d = {a, b, c} 
  ```

- 移位运算符

  - 移位运算符用于将左边操作数左移或右移指定的位数！移位后空闲位用0填充。

    左移运算符： <<

    如： 4‘b1101 << 3 结果为：4‘b1000

  - 右移算法符:   >>

    如： 4‘b1101 >> 3 结果为：4‘b0001 

  - 移位运算符其他用途：左移一位可以看成是乘以 2，右移一位可以看成是除以 2。
    移位运算符代替乘除法可以节省资源！

## 模块

(1) 介绍（和main类似）

```
module  top_module(
    input a,
    input b,
    output out
);
 
   ....... 
 
endmodule
```

(2) 模块实例化

```
mux2_1      mux2_1_inst
(
   .in_1(in_1),   //输入信号1，.表示连接
   .in_2(in_2),   //输入信号2
   .sel(sel),    //选通信号
   .out(out)    //输出信号
);
```

- 按mod_a定义的端口顺序实例化: mod_a instance1 (a, b, out);
- 按mod_a端口名实例化: mod_a instance2 (.in1(a), .in2(b), .out(out));  (推荐此种写法)



## 逻辑块

- always

  ```verilog
  // 2.1always逻辑块
  //  always块可构建 组合逻辑块 和 时序逻辑块，复杂的逻辑操作都需要处于该逻辑块中，如if、case、for等
  
  // 2.1.1组合逻辑块
  // always逻辑块中任意信号变化时立即触发，执行begin - end之间的语句
  // begin - end用于将多条语句组成一个代码块，只有一条语句时可省略
  module top_module();
   
      always @(*) begin
          //....
      end
   
  endmodule
  
  // 2.1.2 时序逻辑电路
  // clk 信号的上升沿触发
  // posedge:  上升沿
  // negedge: 下降沿
  module top_module();
   
      always @(posedge clk) begin
          // ....
      end
   
  endmodule
  
  ```

- generate

  ```verilog
  // 2.2 generate逻辑块
  /*
  generate主要结合for循环使用，主要用途有：
  
  对向量中的多个位进行重复操作
  对同一个模块进行多次重复实例化(主要用途)
  */
  // 2.2.1 操作向量
  module top_module(input [7:0] in,  output [7:0] out);
      genvar i;        // genvar i; 也可以定义在generate内部
      generate
          for(i=0; i<8; i++) begin: bit
               assign out[i]=^in[8-1:i];
          end
      endgenerate
  endmodule
  
  // 模块重复多次实例化
  module  top_module(
      input a,
      input b,
      output out
  );
      genvar i;
      generate
          for(i=0; i<8; i++)  begin: gen_mod_a   //  gen_mod_a 为每个begin_end的结构的名称
              mod_a instance2 (.in1(a), .in2(b), .out(out));
          end
      endgenerate
  endmodule
  ```

  

- initial块 

  ```verilog
  // initial块
  //  initial块可以理解为一个初始化块，在initial的起始位置的语句在0时刻即开始执行，之后如果遇到延时，则延时之后执行接下来的语句。
  // 初始块是不可综合的，因此不能将其转化为带有数字元素的硬件原理图。因此初始块除了在仿真中使用外，并没有太大的作用。
  initial                                                
  begin                                                  
      sys_clk    = 1'b1;                
      sys_rst_n  = 1'b0; 
  	#50
  	sys_rst_n  = 1'b1;                
  end  
  ```

  

## 系统函数

- `timescale 1ns**/**1ns //时间尺度预编译指令 时间单位/时间精度

  仿真中使用“**#**数字”表示延时相应时间单位的时间，例**#**10表示延时10个单位的时间，即10ns。

  ```verilog
  always #10 in_1 <=  {$random} % 2;
  always #10 in_2 <=  {$random} % 2;
  always #10 sel <=  {$random} % 2;
  ```

  时间单位不能比时间精度小

- $display //打印信息，自动换行

  $display**(**“%b+%b=%d”**,**a**,** b**,** c**);**//格式“%b+%b=%d” 格式控制，未指定时默认十进制

  **%**h或**%**H //以十六进制的形式输出

  **%**d或**%**D //以十进制的形式输出

  **%**o或**%**O //以八进制的形式输出

  **%**b或**%**B //以二进制的形式输出

- $write //打印信息

  $write**(**“%b+%b=%dn”**,**a**,** b**,** c**);** //“%b+%b=%dn” 格式控制，未指定时默认十进制

  **%**h或**%**H //以十六进制的形式输出

  **%**d或**%**D //以十进制的形式输出

  **%**o或**%**O //以八进制的形式输出

  **%**b或**%**B //以二进制的形式输出

  \n //换行

- $strobe //打印信息，自动换行，最后执行

  $strobe**(**“%b+%b=%d”**,**a**,**b**,**c**);** //“%b+%b=%d” 格式控制，未指定时默认十进制

  **%**h或**%**H //以十六进制的形式输出

  **%**d或**%**D //以十进制的形式输出

  **%**o或**%**O //以八进制的形式输出

  **%**b或**%**B //以二进制的形式输出

- $monitor //监测变量

  $monitor**(**“%b+%b=%d”**,**a**,**b**,**c**);** //“%b+%b=%d” 格式控制，未指定时默认十进制

  **%**h或**%**H //以十六进制的形式输出

  **%**d或**%**D //以十进制的形式输出

  **%**o或**%**O //以八进制的形式输出

  **%**b或**%**B //以二进制的形式输出

  ```verilog
  always #10 in_1 <=  {$random} % 2;
  always #10 in_2 <=  {$random} % 2;
  always #10 sel <=  {$random} % 2;
  
  initial
      begin
          $timeformat(-9,0,"ns",6);
          $monitor("@time %t:in_1=$b in_2=%b sel=%b out=%b",$time,in_1,in_2,sel,out);
      
      end
  ```

  仿真结果（部分）

  ```
  # @time    0ns:in_1=$b in_2=0 sel=0 out=00
  # @time   10ns:in_1=$b in_2=0 sel=1 out=10
  # @time   20ns:in_1=$b in_2=1 sel=1 out=11
  # @time   30ns:in_1=$b in_2=1 sel=0 out=11
  # @time   60ns:in_1=$b in_2=0 sel=1 out=01
  # @time   70ns:in_1=$b in_2=1 sel=1 out=01
  # @time   80ns:in_1=$b in_2=1 sel=0 out=00
  # @time   90ns:in_1=$b in_2=0 sel=1 out=01
  # @time  100ns:in_1=$b in_2=1 sel=1 out=11
  # @time  110ns:in_1=$b in_2=1 sel=0 out=00
  # @time  120ns:in_1=$b in_2=0 sel=0 out=10
  ```

  

- $stop //暂停仿真

- $finish //结束仿真

- $time //时间函数

- $random //随机函数

- $readmemb //读文件函数
