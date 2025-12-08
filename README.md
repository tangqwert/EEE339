# EEE339
## Q&A
1. Q: 什么是编译器？
   
   A:   

3. Q: 什么是汇编器
   
   A:

5. Q: 机器语言的优势
   
   A: 1. 允许程序员使用更自然地语言进行思考
      2. 语言可以根据其预期用途进行设计
      3. 可在具有不同指令集架构(ISA)的不同平台进行移植

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

20. Q: CPU时钟周期表达式

    A: Instruction count(IC/指令数) * Cycles Per Instruction(CPI/每个指令所需周期数)

21. Q: Average CPI， 平均时钟周期 

    A: 平均时钟周期等于总CPU周期/总指令数

22. Q: 什么是指令集

    A: repertoire of instructions of a computer/计算机的指令库

23. Q: Regdst(Register Destination - 目标寄存器选择) / AluSrc (ALU Source - ALU 数据源选择)

    A:



























    

    



