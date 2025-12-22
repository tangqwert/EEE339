# EEE339
## 目录
- [1. 简介](#简介)
- [2. Q&A](#qa)
- [3.笔记](#笔记)
- [4.单词](#单词)

## 简介
## Q&A
1. Q: 什么是编译器？
   
   A:   

3. Q: 什么是汇编器
   
   A:

5. Q: 机器语言的优势
   
   A: 1. 允许程序员使用更自然地语言进行思考
   
      2. 语言可以根据其预期用途进行设计
            
      4. 可在具有不同指令集架构(ISA)的不同平台进行移植

7. Q:pytorch 是什么

   A:用来做深度学习/神经网络的开源框架

9. Q: OS, ISA, RISC, CISC 是什么？

   A:操作系统， Instruction set architecture指令集架构， 精简指令集计算机，复杂指令集计算机

11. Q: 什么是指令集架构(ISA)?

    A: 1. 汇编语言程序员或者编译器眼中计算机系统属性。包括指令集可以执行哪些操作？指令格式？数据储存在哪里？寻址方式，如何访问数据？以及异常情况处理。
    
      2. 硬件与最底层软件的抽象接口
         
13. Q:现代化指令集架构有哪些？

    A: x86, PowerPC, DEC, Alpha, MIPs, SPARC, ARM, RISC-V

15. Q: 抽象系统构(Abstraction system)成有哪些？

    A: 应用层 > 操作系统 > 指令集 > CPU > Circuit

### 计算机组织结构

9. Q: 处理器结构作用

   A: 数据通路与控制，执行算数与逻辑运算以及向其他组件发出指令。

11. Q: 内存作用

    A: 用于保存数据与指令，缓存，主内存，磁盘

13. Q: 输入结构作用

    A: 向计算机发送数据，键盘，鼠标

15. Q: 输出结构作用

    A: 从计算机获取数据，屏幕，声卡，打印机


16. Q: 什么是相对性能

    A: 性能 = 1 / 执行时间(Execution Time), 性能之比即为相对性能

17. Q: 什么是执行时间？

    A: 经过的时间(elapsed time) 以及 CPU时间

18. Q: 什么是经过时间(elapsed time)？

    A: 总响应时间，包括处理/ I/O / Os开销 / 空闲时间(idle time)

19. Q: 什么是CPU时间？

    A: 1. 处理特定任务所花费的时间，不包括等待I/O或者运行其他程序的时间， 包括用户CPU时间以及系统CPU时间，不同的程序受CPU和系统性能的影响程度也不同。
    
       2. CPU时间 = CPU时钟周期(CPU clock cycles) * CPU单周期时间(Clock cycle time) = CPU时钟周期(CPU clock cycles) / CPU时钟频率(Clock rates)

21. Q: CPU时钟周期表达式

    A: Instruction count(IC/指令数) * Cycles Per Instruction(CPI/每个指令所需周期数)

22. Q: Average CPI， 平均时钟周期 

    A: 平均时钟周期等于总CPU周期/总指令数

23. Q: 什么是指令集

    A: repertoire of instructions of a computer/计算机的指令库

24. Q: Regdst(Register Destination - 目标寄存器选择) / AluSrc (ALU Source - ALU 数据源选择)

    A:

25. Q: MIPS 架构的指令格式有哪些？

    A: 1. R-Format(ADD) 寄存器型  MIPS汇编语言中最常见的指令格式，用于算数运算，逻辑运算，寄存器间数据传输等操作。 格式: opcode(6 bits) | rs(5 bits) | rt(5 bits) | rd(5 bits) | shamt(5 bits) | funct(6 bits) //shamt: 位移量shift amount, funct: 决定加法还是减法
    
       2. I-Format 立即数型 格式: opcode(6 bits) | rs(5 bits) | rt(5 bits) | Immediate(16 bits)
          
       4. J-format 跳转型 格式: opcode(6 bits) | Address(26 bits)

## 笔记
**1. Representation of digital circuit in verilog**

->Structural: use verilog constructs 使用Verilog结构

    Example1: 

         AND gate --> and (y, x1, x2)

         OR gate  --> or (y, x1, x2, x3, x4)
         
         NOT gate --> not (y, x)
         
    Example2:

      module example(x1,x2,x3,f);
         input(x1,x2,x3);
         output(f);

         and (g, x1. x2);
         not (k, x2);
         and (h, k, x3);
         or (f, g, h);
         
      endmodule

   

->Behavioral: use logic expressions and c-like programming construsts define the behaviour of the circuit. 使用逻辑表达式与类似C的结构定义 

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
               
**2. 过程语句(Procedural Statements)**

**3. 并行语句(Concurrent statements)**
   
**4. Identifiers**

   Names of variables and elements
   
**5. Logic Values**

   Four logic values:
   
     0 = logic value 0
     1 = logic value 1
     z, Z, or ? = tri-state (high imoedance or floating) 高阻态/
     x or X = unknown or uninitialized 未知

**6.  Numbers: default 32 bits**

        10 = 10 = 0...01010(32bits)

   D/d decimal       

        4'd3 = 3 = 0011

   H/h hexadecimal

        8'ha = 10 = 00001010

   O/o octal

   B/b binary

        5'b111 = 7 = 00111

**7. Data Types:**

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

**8. Operators**
1. Arithmetic Operators

   + m+n add n to m

   - m-n subtract n from m
  
   - -m negate m (2's complement)
  
   * m*n Multiply m by n
  
   / m/n Divide m by n

    % m%n Modulus of m/n, the result takes the sign of the first operand, e.g.

       5 % 2 = 1
       5 % -2 = 1
       -5 % 2 = -1
       -5 % -2 = -1
   
2. bitwise operators

   ~ ~m Invert each bit of m (1’s complement)

   & m&n AND each bit of m with each bit of n

   | m|n OR each bit of m with each bit of n

   ^ m^n Exclusive OR each bit of m with n

   ~^ m ~^ n Exclusive NOR each bit of m with n
   
   ^~ m ^~ n Exclusive NOR each bit of m with n

3. logical Operators (1-bit T/F result)

   ! !m Is m false?

   && m && n Are both m and n true?

   || m || n Is either m or n true?

4. Reduction Operators 归约运算符 (1-bit T/F result): calculated by recursively applying bit-wise operation on all bits.

   & &m AND all bits in m together

   ~& ~&m NAND all bits in m together

   | |m OR all bits in m together

   ~| ~|m NOR all bits in m together //检查总线状态，全输出为0是，输出为1

   ^ ^m Exclusive OR all bits in m  //奇偶性检查

   ~^ ~^m Exclusive NOR all bits in m

   ^~ ^~m Exclusive NOR all bits in m

5. Relational Operators 关系运算符 (1-bit T/F result)

   < m < n Is m less than n?

   > m > n Is m greater than n?
   
   <= m <= n Is m less than or equal to n?

   >= 大于等于 m >= n Is m greater than or equal to n?

   == 逻辑相等 m == n Is m equal to n? //模拟硬件电路的行为。如果你问它 4'b10x0 == 4'b10x0，它会告诉你 结果是 x (未知)。因为硬件不知道那个 x 到底是 0 还是 1，所以无法判断是否相等。

   != 逻辑不等 m != n Is m not equal to n?

   === 全等 m===n is m identical to n? //模拟软件字符串匹配的行为。如果你问它 4'b10x0 === 4'b10x0，它会告诉你 1 (真)。因为它认为左边的 x 和右边的 x 长得一样。

   !== 全不等 m!==n is m not identical to n?

6. Logical Shift Operators

   << m << n Shift m left n-times

   >> m >> n Shift m right n-times //The vacant bits are filled with 0

7. Arithmetic Shift Operators

   <<< m <<< n Shift m left n-times, the vacant bits are filled with 0.

   >>> m >>> n Shift m right n-times, the vacant bits are filled with the leftmost bit (the sign bit for a signed integer).

       integer a, b, c; // signed data types
       a = -8; // a = 11…11000
       b = a >>> 3; // b = 11…11111 , b = -1 decimal
       c = a <<< 2; // b = 11…1100000, b = -32 decimal 12
       
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

**9. **
## 单词
1. Primitives 原语，基本元素
   
2. tedious 单调乏味的

3. concurrent 并发的
   
4. lexical 词汇的
   
5. conventions 协议
    
6. identifiers 标识符

7. ternary 三元的

8. Concatenate 连接

9. Precedence 优先级














































    

    



