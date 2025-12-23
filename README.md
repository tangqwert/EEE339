# EEE339 学习笔记

> 本笔记用于系统整理 EEE339 课程中的核心概念、ISA 基础与 Verilog 硬件描述语言内容，适合作为复习与查阅资料。
>  https://hdlbits.01xz.net/wiki/Exams/m2014_q4j
---

## 目录
- [1. 课程简介](#1-课程简介)
- [2. 核心概念 Q&A](#2-核心概念-qa)
  - [2.1 语言与系统层次](#21-语言与系统层次)
  - [2.2 计算机组织结构](#22-计算机组织结构)
  - [2.3 性能与指标](#23-性能与指标)
  - [2.4 MIPS 与 ISA](#24-mips-与-isa)
- [3. Verilog 笔记](#3-verilog-笔记)
  - [3.1 电路建模方式](#31-电路建模方式)
  - [3.2 语句类型](#32-语句类型)
  - [3.3 标识符与逻辑值](#33-标识符与逻辑值)
  - [3.4 数值表示](#34-数值表示)
  - [3.5 数据类型](#35-数据类型)
  - [3.6 运算符系统](#36-运算符系统)
  - [3.7 寄存器](#37-寄存器)
- [4. 单词表](#4-单词表)

---

## 1. 课程简介

EEE339 主要介绍计算机系统的抽象层次、指令集架构（ISA）、性能评估方法，以及 Verilog 硬件描述语言的基础用法。

---

## 2. 核心概念 Q&A

### 2.1 语言与系统层次

**Q：什么是编译器（Compiler）？**  
- 将高级语言程序翻译为机器语言的工具。

**Q：什么是汇编器（Assembler）？**  
- 将汇编语言翻译为机器语言的工具。

**Q：高级语言相对于机器语言的优势？**
1. 更符合人类思维方式  
2. 可针对用途设计语言  
3. 具有良好可移植性  

**Q：PyTorch 是什么？**  
- 一个用于深度学习与神经网络的开源框架。

**Q：OS、ISA、RISC、CISC 分别是什么？**
- **OS**：Operating System  
- **ISA**：Instruction Set Architecture  
- **RISC**：Reduced Instruction Set Computer  
- **CISC**：Complex Instruction Set Computer  

**Q：什么是 ISA？**
1. 汇编程序员或编译器眼中的计算机  
2. 硬件与底层软件之间的抽象接口  
3. 定义指令、寄存器、数据格式与异常处理机制  

**Q：常见现代 ISA？**
- x86, ARM, MIPS, RISC-V, PowerPC, SPARC, DEC Alpha

**Q：计算机抽象层次结构？**
- **A:** 应用层 $\rightarrow$ 操作系统 $\rightarrow$ 指令集 $\rightarrow$ CPU $\rightarrow$ 电路。


---

### 2.2 计算机组织结构

**Q：处理器的作用？**
- 执行算术与逻辑运算  
- 控制数据通路  
- 向其他部件发出控制信号  

**Q：内存的作用？**
- 存储数据与指令  
- 包括 Cache、Main Memory、Disk  

**Q：I/O 结构的作用？**
- 输入设备：键盘、鼠标  
- 输出设备：显示器、打印机  

---

### 2.3 性能与指标

**Q：什么是性能（Performance）？**
\[
Performance = \frac{1}{Execution\ Time}
\]

**Q：什么是执行时间（Execution Time）？**
- 包括 Elapsed Time 与 CPU Time  

**Q：Elapsed Time 是什么？**
- 程序的总响应时间  
- 包含 I/O、OS 开销与空闲时间  

**Q：CPU Time 是什么？**
\[
CPU\ Time = \frac{CPU\ clock\ cycles}{Clock\ rate}
\]

**Q：CPU 时钟周期公式**
\[
CPU\ clock\ cycles = IC \times CPI
\]

**Q：平均 CPI**
\[
Average\ CPI = \frac{Total\ CPU\ cycles}{Total\ Instruction\ Count}
\]

---

### 2.4 MIPS 与 ISA

**Q：什么是指令集（Instruction Set）？**
- 处理器支持的指令集合

**Q：MIPS 指令格式有哪些？**

**R-Format**
- **A:** 1. **R-Format (寄存器型):** `opcode(6) | rs(5) | rt(5) | rd(5) | shamt(5) | funct(6)`
      2. **I-Format (立即数型):** `opcode(6) | rs(5) | rt(5) | Immediate(16)`
      3. **J-Format (跳转型):** `opcode(6) | Address(26)`

---

## 3. 笔记

### 3.1. Verilog 电路表示法
- **Structural (结构化):** 使用原语描述物理连接。
  ```verilog
  and (y, x1, x2);
  or (y, x1, x2, x3, x4);
  not (y, x);

  //example2
  module example(x1, x2, x3, f);
    input x1, x2, x3;
    output f;
    wire g, k, h;

    and (g, x1, x2);
    not (k, x2);
    and (h, k, x3);
    or  (f, g, h);
  endmodule
   

- **Behavioral:** use logic expressions and c-like programming construsts define the behaviour of the circuit. 使用逻辑表达式与类似C的结构定义 
  ```verilog
    Example1:
    module example3(x1,x2,x3,f);
     input x1, x2, x3;
     output f;

     assign f= (x1 & x2) | (~x2 & x3);
    endmodule

    Example2:
    module example(x1,x2,x3,x4, g, f, h);
     input x1, x2, x3, x4;
     output g, f, h;

     assign g = (x1 & x3) |(x2 & x4);
     assign h = (x1 | ~x3) & (~x2 | x4);
     assign f = g | h;
    
    endmodule
               
### 3.2 过程语句（Procedural Statements）
> 用于描述“随时间/触发条件变化”的硬件行为，通常写在 `always` 块中。  
> 常见用途：时序逻辑（寄存器/触发器）、组合逻辑（用 always 模拟）。

- 常见触发方式：
  - 组合逻辑：`always @(*)`
  - 时序逻辑：`always @(posedge clk)` / `always @(negedge clk)`
- 常见赋值（取决于课程要求/工具链）：
  - 阻塞赋值：`=`
  - 非阻塞赋值：`<=`

---

### 3.3 并发语句（Concurrent Statements）
> 并发语句表达“电路连线/组合逻辑”的持续驱动关系，最典型是 `assign`。

- 常见写法：
  - `assign y = a & b;`
  - `assign y = (sel) ? d1 : d0;`

---

### 3.4 Identifiers（标识符）
> 用于命名变量、模块、端口、信号线等。

- **Identifiers**：Names of variables and elements

---

### 3.5 Logic Values（逻辑值）
Verilog 使用四值逻辑（4-state logic）：

| 取值 | 含义（English） | 含义（中文） |
|---|---|---|
| `0` | logic value 0 | 逻辑 0 |
| `1` | logic value 1 | 逻辑 1 |
| `z` / `Z` / `?` | tri-state (high impedance / floating) | 三态/高阻/悬空 |
| `x` / `X` | unknown / uninitialized | 未知/未初始化 |

---

### 3.6 Numbers（数值表示，默认 32 bits）
- 默认：**32-bit**（若不显式指定位宽）

**示例：**
```verilog
10       // 十进制 10，默认扩展为 32-bit：0...01010
4'd3     // 4 位十进制 3：0011
8'hA     // 8 位十六进制 A(10)：00001010
5'b111   // 5 位二进制 111(7)：00111

```



### 3.7 Data Types:

   1. net: represemts interconnection between structural entities such as gates

      Format:  net_type [size] net_name , net_name , ...;
      
      size: the range of [msb : lsb]
  
          1. wire: used to connect an output of one logic element to an input of another logic element
             wire x;
          2. tri:  used for tri-state circuit nodes
             tri[7:0] DataOut;
  
   3. register: stores a value from one assignment to the next. In Verilog, the term register only means a variable
      that can hold a value until another value is placed onto it.
      
      Format: register_type[size] variable_name, variable_name, ...;
      
      size: ...

          1. reg: unsigned variable of any bit size to be defined
            reg [2:0] Count; //3-bit unsigned variable
          2.integer: signed 32-bit variable
            integer k; // 32-bit signed variable
  
   5. memory: one-dimensional array of registers

      Format: register_type [size] memory_name [array_size]

      array_size: the range of [first_address : last_address]; either ascending or descending address order may be used

          a=reg [7:0] R [3:0]; //declare four 8-bit variables
          R[3] //access the individual variable
          R[3][7] //access the left most bit of R[3]
      
   7. parameter: define constants

      Format: parameter constant_name = value;

      constant_name = value,...;

          module addern(carryinm, X, Y, S);
            parameter n = 32;
            input carryin;
            input[n-1:0] X, Y;
            output reg [n-1:0] S;
      
            always@(X,Y,carryin)
                  S=X+Y+carryin
          endmodule

## 3.8 Operators（运算符）

---

### 3.8.1 Arithmetic Operators（算术运算符）

| 运算符 | 表达式 | 含义 |
|---|---|---|
| `+` | `m + n` | 加法 |
| `-` | `m - n` | 减法 |
| `-` | `-m` | 取负（二进制补码） |
| `*` | `m * n` | 乘法 |
| `/` | `m / n` | 除法 |
| `%` | `m % n` | 取模（符号取决于第一个操作数） |

**取模示例：**

       5 % 2 = 1
       5 % -2 = 1
       -5 % 2 = -1
       -5 % -2 = -1
   

---

### 3.8.2 Bitwise Operators（按位运算符）

| 运算符 | 表达式 | 含义 |
|---|---|---|
| `~` | `~m` | 按位取反（1's complement） |
| `&` | `m & n` | 按位与 |
| `|` | `m | n` | 按位或 |
| `^` | `m ^ n` | 按位异或 |
| `~^` / `^~` | `m ~^ n` | 按位同或（XNOR） |

---

### 3.8.3 Logical Operators（逻辑运算符，1-bit 结果）

> 逻辑运算符 **只关心 True / False**，结果始终是 **1-bit**。

| 运算符 | 表达式 | 含义 |
|---|---|---|
| `!` | `!m` | 逻辑非 |
| `&&` | `m && n` | 逻辑与 |
| `||` | `m || n` | 逻辑或 |

---

### 3.8.4 Reduction Operators（归约运算符，1-bit 结果）

> 对一个向量的**所有位**进行递归按位运算，常用于校验或总线检测。

| 运算符 | 表达式 | 含义 | 常见用途 |
|---|---|---|---|
| `&` | `&m` | 归约与 | 检查是否全为 1 |
| `~&` | `~&m` | 归约与非 | |
| `|` | `|m` | 归约或 | 是否存在 1 |
| `~|` | `~|m` | 归约或非 | 检查总线是否全 0 |
| `^` | `^m` | 归约异或 | 奇偶校验 |
| `~^` / `^~` | `~^m` | 归约同或 | |

---

### 3.8.5 Relational & Equality Operators（关系 / 相等运算符）

> ⚠️ **考试重点：`==` 与 `===` 的区别**

| 运算符 | 表达式 | 含义 |
|---|---|---|
| `<` | `m < n` | 小于 |
| `>` | `m > n` | 大于 |
| `<=` | `m <= n` | 小于等于 |
| `>=` | `m >= n` | 大于等于 |
| `==` | `m == n` | 逻辑相等（遇到 `x/z` 可能返回 `x`） |
| `!=` | `m != n` | 逻辑不等 |
| `===` | `m === n` | 全等（逐位比较，`x/z` 也参与） |
| `!==` | `m !== n` | 全不等 |

**关键理解：**
- `==`：模拟硬件比较  
  - `4'b10x0 == 4'b10x0 → x`
- `===`：逐位严格比较  
  - `4'b10x0 === 4'b10x0 → 1`

---

### 3.8.6 Shift Operators（移位运算符）

#### Logical Shift（逻辑移位）
| 运算符 | 含义 |
|---|---|
| `<<` | 左移，低位补 0 |
| `>>` | 右移，高位补 0 |

#### Arithmetic Shift（算术移位，用于有符号数）
| 运算符 | 含义 |
|---|---|
| `<<<` | 左移，补 0 |
| `>>>` | 右移，补符号位 |

```verilog
integer a, b, c; // signed
a = -8;          // ...11000
b = a >>> 3;     // ...11111  (-1)
c = a <<< 2;     // ...1100000 (-32)
```

### 3.8.7 Arithmetic Shift Operators（算术移位运算符）

> 算术移位主要用于 **有符号数（signed data）**，右移时会保留符号位。

| 运算符 | 表达式 | 含义 |
|---|---|---|
| `<<<` | `m <<< n` | 左移 n 位，低位补 0 |
| `>>>` | `m >>> n` | 右移 n 位，高位补符号位（sign bit） |

**示例：**
```verilog
integer a, b, c;   // signed data types

a = -8;            // 二进制表示：11...11000
b = a >>> 3;       // 右移补符号位：11...11111  -> -1
c = a <<< 2;       // 左移补 0：11...1100000 -> -32
```
8. Conditional Operator 条件运算符

   condition ? value_if_true : value_if_false //如果条件为真 (1)，选择前者。 如果条件为假 (0)，选择后者。

       **2-to-1 Mux (2选1多路选择器)**:
       * 代码: `assign out = Y ? b : a;`
       * 含义: Y为1输出b，Y为0输出a。
       **Tri-state Buffer (三态缓冲器)**:
       * 代码: `assign out = enable ? in : 16'bz;`
       * 含义: 如果 enable 有效，输出 data；否则输出 **高阻态 (High-Z)**。这是总线设计的核心。
       **Nested (嵌套使用)**:
       * 可以通过嵌套构建更大的 Mux (如 4选1)。
       * 代码: `assign out = X ? (Y ? d : c) : (Y ? b : a);`

9. Concatenation Operator 拼接运算符
    
    Format: `{ , }`
    Example: {operand1, operand2, ...}, y = {1'b1, a};

10. Replication Operator  复制运算符

    Format: `{{}}`
    Example: assign sign_ext_imm = { {16{instruction[15]}}, instruction[15:0] }; // 假设 instruction[15:0] 是 16位立即数. instruction[15] 是符号位 (Sign Bit)

11. 运算符优先级(Precedence)
    
1.  **最高级**: 一元运算 (`!`, `~`, `&m` 等)
2.  **算术**: `*`, `/` > `+`, `-`
3.  **移位**: `<<`, `>>`
4.  **关系**: `<`, `>`
5.  **相等**: `==`, `!=`
6.  **按位**: `&` > `^` > `|`
7.  **逻辑**: `&&` > `||`
8.  **最低级**: 条件 `? :`


## 3.7 锁存器&触发器 ##
-** sequential vs combinational**

|sequential 时序逻辑 | combinational 组合逻辑 |
|输出由**当前输入与过去状态共同决定**|输出由当前输入决定|

** 储存状态的元件 **
|latch 锁存器|flip-flop 触发器|
|level sensitive|edge sensitive|

## latch ##

1. ** SR latch **
   (a) SR high active

   |S|R|Q(next)|Meaning|
   |0|0|Q(Prev)|Hold保持|
   |1|0|1|Set 1|
   |0|1|0|Reset(set 0)|
   |1|1|?|Invalid/Forbidden非法|

   (b) SR low active
   invert

2. ** D latch **

   |D|E|Q(next)|
   |D|1|D|
   |D|0|Q(Pre)|


## Flip-flops ##

1. **D Filp-flop**
  最常用，寄存器本质就是大量 DFF。

  在时钟边沿：Q(next)=D

  其余时间：Q 保持
   ```veilog
   always @(posedge clk) Q <= D;
```

2. **T flip-flop**
   输入 T 控制是否翻转。

   | T | Q(next)  |
   | - | -------- |
   | 0 | Q(prev)  |
   | 1 | ~Q(prev) |

   公式：

   Q+=Q⊕T
3. **JK Flip-flop**
   可以看成“无非法态”的 SR flip-flop，且 J=K=1 时翻转。
   
| J | K | Q(next)  | Meaning |
| - | - | -------- | ------- |
| 0 | 0 | Q(prev)  | Hold    |
| 1 | 0 | 1        | Set     |
| 0 | 1 | 0        | Reset   |
| 1 | 1 | ~Q(prev) | Toggle  |

公式（常用形式之一）：
Q+=JQ​'+ K'Q
   









**9. **
## 单词
1. Primitives 原语，基本元素
   
2. tedious 单调乏味的

3. concurrent 并发的
     |1|1|?|Invalid/Forbidden非法|
ons 协议
    
6. identifiers 标识符

7. ternary 三元的

8. Concatenate 连接

9. Precedence 优先级

10. Instantiations 实例化

11. overriding 覆盖

12. explicit 显性

13. iteration 迭代

14. asynchronous 异步

15. synchronous 同步

16. consequence 结果后果












```verilog
module TFF (
input t,
input clk,
input rst,
output reg q
);
always @(posedge clk or posedge rst)
if (rst) begin
  q <= 1'b0;
end else if (t) begin
  q <= ~q;
end
end
endmodule

module scounter (
input Vcc,
input CLK,
input Rst,
output Tc
);

wire [3:0] Q;

TFF tff1 (
  .t (Vcc),
  .clk (CLK),
  .rst (Rst),
  .q (Q[0])
);

TFF tff2(
  .t (Vcc & Q[0]),
  .clk (CLK),
  .rst (Rst),
  .q (Q[1])
);

TFF tff3(
  .t (Vcc & Q[0] & Q[1]),
  .clk (CLK),
  .rst (Rst),
  .q (Q[2])
);

TFF tff4(
  .t (Vcc & Q[0] & Q[1] & Q[2]),
  .clk (CLK),
  .rst (Rst),
  .q (Q[3])
);

assign Tc = Vcc & Q[0] & Q[1] & Q[2] & Q[3];

endmodule


























    

    



