---
title: FPGA基础
category: FPGA
abbrlink: 5241b77d
date: 2023-05-26 14:01:45
tags:
swiper_index:
keywords:
cover:
highlight_shrink:
---

——转载自[野火](https://doc.embedfire.com/fpga/altera/ep4ce10_pro/zh/latest/index.html)

## 软件安装

- Quartus ||

  Altera公司开发的综合CPLD/FPGA开发软件

- usb-blaster

  下载器

- modelsim

  仿真软件

- visio

- 编辑器



## Modelsim仿真软件问题

1. 出现下述错误

   ![image-20230602183242810](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230602183242810.png)

   仿真结果表现为，高阻态（蓝色），和无常态（红色）

   修改：下述框的第二个框，必须与建立module名一致，

   ![image-20230602183402289](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230602183402289.png)



## 多路选择器

```verilog
module  mux2_1
(
    input   wire    [0:0]   in_1,   //输入信号1
    input   wire            in_2,   //输入信号2
    input   wire            sel,    //选通信号
    
    output  reg             out     //输出信号
);

always@(*)  //  *为通配符，所有信号变化都执行
    if(sel == 1'b1)
        out = in_1;
    else    
        out = in_2;
     
always@(*)
    case(sel)
        1'b1    :out = in1;
        1'b0    :out = in2;
        default :out = in1;
    endcase

   
assign  out = (sel == 1'b1) ? in1 : in2;
   
endmodule
```

仿真代码

```verilog
`timescale 1ns/1ns  // 系统函数

module tb_mux2_1();

reg     in_1;
reg     in_2;
reg     sel ;

wire    out ;

initial
    begin
        in_1    <=  1'b0;
        in_2    <=  1'b0; 
        sel     <=  1'b0;
    end

always #10 in_1 <=  {$random} % 2;
always #10 in_2 <=  {$random} % 2;
always #10 sel <=  {$random} % 2;

initial
    begin
        $timeformat(-9,0,"ns",6);
        $monitor("@time %t:in_1=$b in_2=%b sel=%b out=%b",$time,in_1,in_2,sel,out);
    
    end

mux2_1      mux2_1_inst
(
   .in_1(in_1),   //输入信号1，.表示连接
   .in_2(in_2),   //输入信号2
   .sel(sel),    //选通信号
   .out(out)    //输出信号
);

endmodule
```





## 译码器

3-8译码器

```verilog
module  decoder
(
    input   wire        in_1,
    input   wire        in_2,
    input   wire        in_3,
    
    output  reg   [7:0] out 
);

/* always@(*)
    if({in_1,in_2,in_3} == 3'b000)
        out = 8'b0000_0001;
    else    if({in_1,in_2,in_3} == 3'b001)
        out = 8'b0000_0010;
    else    if({in_1,in_2,in_3} == 3'b010)
        out = 8'b0000_0100;
    else    if({in_1,in_2,in_3} == 3'b011)
        out = 8'b0000_1000;
    else    if({in_1,in_2,in_3} == 3'b100)
        out = 8'b0001_0000;
    else    if({in_1,in_2,in_3} == 3'b101)
        out = 8'b0010_0000;
    else    if({in_1,in_2,in_3} == 3'b110)
        out = 8'b0100_0000;
    else    if({in_1,in_2,in_3} == 3'b111)
        out = 8'b1000_0000;
    else    
        out = 8'b0000_0001; */
        
always@(*)
    case({in_1,in_2,in_3} )
        3'b000:out = 8'b0000_0001;
        3'b001:out = 8'b0000_0010;
        3'b010:out = 8'b0000_0100;
        3'b011:out = 8'b0000_1000;
        3'b100:out = 8'b0001_0000;
        3'b101:out = 8'b0010_0000;
        3'b110:out = 8'b0100_0000;
        3'b111:out = 8'b1000_0000;
        default:out = 8'b0000_0001;
    endcase
        
                 
endmodule
```



仿真代码

```verilog
`timescale 1ns/1ns

module tb_decoder();

reg        in_1;
reg        in_2;
reg        in_3;
    
wire   [7:0] out ;

initial
    begin
        in_1 <= 1'b0;
        in_2 <= 1'b0;
        in_3 <= 1'b0;
    end

always #10 in_1 <= {$random} % 2;
always #10 in_2 <= {$random} % 2; 
always #10 in_3 <= {$random} % 2; 

initial
    begin
        $timeformat(-9,0,"ns",6);
        $monitor("@time %t:in_1=$b in_2=%b in_3=%b out=%b",$time,in_1,in_2,in_3,out);
    end

decoder decoder_inst
(
    .in_1(in_1),
    .in_2(in_2),
    .in_3(in_3),
    
    .out(out)
);       

endmodule
```



## 半加器

```verilog
module  half_adder
(
    input   wire    in_1,
    input   wire    in_2,
    output  wire    sum,
    output  wire    count

);
assign  {count,sum} = in_1+in_2;

endmodule
```



仿真

```verilog
`timescale  1ns/1ns
module  tb_half_adder();

reg    in_1;
reg    in_2;

wire    sum;
wire    count;

initial
    begin
        in_1    <=  1'b0;
        in_2    <=  1'b0;
    end

always #10 in_1    <=  {$random}%2;
always #10 in_2    <=  {$random}%2;

initial
    begin
        $timeformat(-9,0,"ns",6);
        $monitor("@time %t:in_1=$b in_2=%b sum=%b count=%b",$time,in_1,in_2,sum,count);
    end

half_adder  half_adder_inst
(
    .in_1(in_1),
    .in_2(in_2),
    .sum(sum),
    .count(count)

);

endmodule

```



## 全加器

逻辑图

![image-20230529213154364](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230529213154364.png)

```verilog
module  full_adder
(
    input   wire    in_1,
    input   wire    in_2,
    input   wire    cin,
    
    output  wire    sum,
    output  wire    count

);

wire    h0_sum;
wire    h0_count;
wire    h1_count;

half_adder  half_adder_inst0
(
    .in_1(in_1),
    .in_2(in_2),
    .sum(h0_sum),
    .count(h0_count)
);

half_adder  half_adder_inst1
(
    .in_1(h0_sum),
    .in_2(cin),
    .sum(sum),
    .count(h1_count)
);

assign  count = {h0_count | h1_count};

endmodule
```



测试

```verilog
`timescale  1ns/1ns
module  tb_full_adder();

reg    in_1;
reg    in_2;
reg    cin;

wire    sum;
wire    count;

initial
    begin
        in_1    <=  1'b0;
        in_2    <=  1'b0;
        cin    <=  1'b0;
    end

always #10 in_1    <=  {$random}%2;
always #10 in_2    <=  {$random}%2;
always #10 cin    <=  {$random}%2;

initial
    begin
        $timeformat(-9,0,"ns",6);
        $monitor("@time %t:in_1=$b in_2=%b cin=%b sum=%b count=%b",$time,in_1,in_2,cin,sum,count);
    end

full_adder  full_adder_inst
(
    .in_1(in_1),
    .in_2(in_2),
    .cin(cin),
    .sum(sum),
    .count(count)

);

endmodule

```



## latch

- Latch其实就是锁存器，是一种在异步电路系统中，对输入信号电平敏感的单元，用来存储信息。锁存器在数据未锁存时，输出端的信号随输入信号变化，就像信号通过一个缓冲器，一旦锁存信号有效，则数据被锁存，输入信号不起作用。因此，锁存器也被称为透明锁存器，指的是不锁存时输出对于输入是透明的。

- 异步电路：异步电路主要是组合逻辑电路，用于产生ＦＩＦＯ或ＲＡＭ的读写控制信号脉冲，但它同时也用在时序电路中，此时它没有统一的时钟，状态变化的时刻是不稳定的，通常输入信号只在电路处于稳定状态时才发生变化。

- 同步电路：同步电路是由时序电路(寄存器和各种触发器)和组合逻辑电路构成的电路，其所有操作都是在严格的时钟控制下完成的。这些时序电路共享同一个时钟ＣＬＫ，而所 有的状态变化都是在时钟的上升沿(或下降沿)完成的。

- 同步电路中latch危害：

  对毛刺敏感；不能异步复位，上电后处于不定态；还会让静态时序分析变得十分复杂

- 产生latch的情况

  1. 组合逻辑中if语句没有else；
  2. 组合逻辑中case的条件不能够完全列举时且不写default；
  3. 组合逻辑中输出变量赋值给自己。

  

## 寄存器

1. 竞争冒险

   在组合电路中，当输入信号的状态发生变化使，输出端可能出现不正常的干扰信号，使电路产生错误输出，这种现象称为竞争冒险。

   ![image-20230601091945726](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230601091945726.png)

​	

2. 寄存器

D触发器的功能为：在一个脉冲信号（一般为晶振产生的时钟脉冲）上升沿或下降沿的作用下，将信号从输入端D送到输出端Q，如果时钟脉冲的边沿信号未出现，即使输入信号改变，输出信号仍然保持原值，且寄存器拥有复位清零功能，其复位又分为同步复位和异步复位。

同步复位D触发器：

![image-20230602185912939](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230602185912939.png)

异步复位D触发器：

![image-20230602185942168](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230602185942168.png)

3. 代码编写

```verilog
module flip_flop
(
    input   wire    sys_clk,
//系统时钟50Mh，后面我们都是设计的时序电路
//所以一定要有时钟，时序电路中几乎所有的信
//号都是伴随着时钟的沿（上升沿或下降沿，习
//惯上用上升沿）进行工作的

    input   wire    sys_rst_n,
//全局复位，复位信号的主要作用是在系统出现
//问题是能够回到初始状态，或一些信号的初始
 //化时需要进行复位
 
    input   wire    key_in,
    
    output  reg     led_out
);
always@(posedge sys_clk) // 同步复位
// always@(posedge sys_clk or negedge sys_rst_n) 异步复位
    if(sys_rst_n == 1'b0)
        led_out <= 1'b0;
    else
        led_out <= key_in;

endmodule
```

4. 测试代码

   ```verilog
   `timescale 1ns/1ns
   /* 时间尺度、精度单位定义，决定“#（不可被综合，但在可
   综合代码中也可以写，只是会在仿真时表达效果，而综合
   时会自动被综合器优化掉）”后面的数字表示的时间尺度和
   精度，具体表达含义为:“时间尺度/时间精度”。为了以后
   编写方便我们将该句放在所有“.v”文件的开头， */
   
   module  tb_flip_flop();
   /* testbench的格式和待测试RTL模块的格式相同
   也是以“module”开始以“endmodule”结束，所有的代码都要
   在它们中间编写。不同的是在testbench中端口列表为空
   因为testbench不对外进行信号的输入输出，只是自己产生
   激励信号提供给内部实例化待测RTL模块使用，所以端口列表
   中没有内容，只是列出“()”，当然可以将“()”省略，括号
   后有个“;”不要忘记 */
   
   //要在initial块和always块中被赋值的变量一定要是reg型
   //在testbench中待测试RTL模块的输入永远是reg型变量
   reg sys_clk;
   reg sys_rst_n;
   reg key_in;
   
   //输出信号，我们直接观察，也不用在任何地方进行赋值
   //所以是wire型变量（在testbench中待测试RTL模块的输出永远是wire型变量）
   wire    led_out;
   
   //initial语句是可以被综合的，一般只在testbench中表达而不在RTL代码中表达
   //initial块中的语句上电后只执行一次，主要用于初始化仿真中要输入的信号
   //初始化值在没有特殊要求的情况下给0或1都可以。如果不赋初值，仿真时信号
   //会显示为不定态（ModelSim中的波形显示红色）
   initial
       begin //在同一个always块中给多个变量赋值的时候要加上
          sys_clk = 1'b1;
          sys_rst_n <= 1'b0;
          key_in   <=  1'b0;
          # 20 //延迟20ns
          sys_rst_n   <=  1'b1;
          # 210
          sys_rst_n   <=  1'b0;
          # 40
          sys_rst_n   <=  1'b1;
       end
   
   always  # 10 sys_clk = ~sys_clk;
   always  # 20 key_in <= {$random}%2; //取模求余数，产生随机数1'b0、1'b1
   
   initial
       begin
           $timeformat(-9,0,"ns",6);
           //设置显示的时间格式，此处表示的是(打印时间单
           //位为纳秒，小数点后打印的小数位为0位，时间值
           //后打印的字符串为“ns”，打印的最小数量字符为6个)
           $monitor("@time %t:key_in=%b  led_out=%b",$time,key_in,led_out);
       
       end
   
   //待测试RTL模块的实例化，相当于将待测试模块放到测试模块中，并将输入输出对应连接上
   //测试模块中产生激励信号给待测试模块的输入，以观察待测试模块的输出信号是否正确
   flip_flop   flip_flop_inst
   //第一个是被实例化模块的名子，第二个是我们自己定义的在另一个
   //模块中实例化后的名字。同一个模块可以在另一个模块中或不同的
   //另外模块中被多次实例化，第一个名字相同，第二个名字不同
   (
   //前面的“sys_clk”表示被实例化模块中的信号，后面的“sys_clk”表示实例化该模块并要和这个
   //模块的该信号相连接的信号（可以取名不同，一般取名相同，方便连接和观察）
   //“.”可以理解为将这两个信号连接在一起
       .sys_clk(sys_clk),
       .sys_rst_n(sys_rst_n),
       .key_in(key_in),
                
       .led_out(led_out)
   );
   
   endmodule
   ```

5. 仿真结果

   

   ![image-20230602190633210](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230602190633210.png)

6. 注意事项

   为什么采用非阻塞赋值

   下图是采用阻塞赋值的形式的仿真

   ![image-20230602190916354](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230602190916354.png)

   明显可以看到输出不会滞后属于一个周期



## 计数器

1. 画时序图

   ![image-20230603120919142](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230603120919142.png)

2. 代码

   ```verilog
   module counter
   #(
       parameter   CNT_MAX = 25'd24_999_999/* 这是我们第一次使用参数的方式定义常量
   使用参数的方式定义常量有很多好处，如：我们在RTL代码中实例化该模块时，如果需要两个
   不同计数值的计数器我们不必设计两个模块，而是直接修改参数的值即可；另一个好处是在编
   写Testbench进行仿真时我们也需要实例化该模块，但是我们需要仿真至少0.5s的时间才
   能够看出到led_out效果，这会让仿真时间很长，也会导致产生的仿真文件很大，所以我们
   可以通过直接修改参数的方式来缩短仿真的时间而看到相同的效果，且不会影响到RTL代码模
   块中的实际值，因为parameter定义的是局部参数，所以只在本模块中有效。为了更好的区
    分，参数名我们习惯上都要大写 */
   )
   
   (
       input   wire    sys_clk,
       input   wire    sys_rst_n,
       
       output  reg    led_out
   
   );
   /* // 参数定义方式
   parameter   CNT_MAX = 25'd24_999_999;
   localparam  CNT_MAX = 25'd24_999_999;  // 局部参数 */
   
   
   reg     [24:0]  cnt;
   
   always@(posedge sys_clk or negedge sys_rst_n)
       if(sys_rst_n == 1'b0)
           cnt <= 25'b0;
       else if(cnt == CNT_MAX)
           cnt <= 25'b0;
       else
           cnt <= cnt + 25'b1 ;
           
   always@(posedge sys_clk or negedge sys_rst_n)
       if(sys_rst_n == 1'b0)
           led_out <= 1'b0;
       else if(cnt == CNT_MAX)
           led_out <= ~led_out;
       else
           led_out <= led_out;
           
   
   // 利用参数实例化举例
   /* counter counter_1
   #(
       .CNT_MAX (100),
   )
   
   (
       .sys_clk   (sys_clk)
       .sys_rst_n (sys_rst_n)
   
       .led_out   (led_out)
   
   );
    */
   
   endmodule
   ```

3. rtl 视图

   ![image-20230605095550311](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/image-20230605095550311.png)



4. 仿真代码

   ```verilog
   `timescale 1ns/1ns
   module tb_counter();
   
   reg     sys_clk;
   reg     sys_rst_n;
   
   wire    led_out;
   
   initial
       begin
           sys_clk = 1'b1;  // 这里脉冲使用阻塞赋值，阻塞赋值优先于非阻塞赋值
           sys_rst_n   <=  1'b0;
           #20
           sys_rst_n   <=  1'b1;
       end
   
   always #10  sys_clk = ~sys_clk;
   
   initial
       begin
           $timeformat(-9,0,"ns",6);
           $monitor("@time %t:led_out = %b",$time,led_out);
       end
       
   counter
   #(
       .CNT_MAX(25'd24)
     ) 
   counter_inst  
   (
       .sys_clk    (sys_clk),
       .sys_rst_n  (sys_rst_n),
       .led_out     (led_out)
   
   );
   
   endmodule
   ```

   
