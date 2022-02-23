step1:
HackCPU has some speed defects. HackCPU have no hardware circuit for multiplication and division. Therefore, subroutines must be written in a combined language to perform multiplication and division, which will make the "multiplication and division" a hundred times slower. The second is the hardware circuit without floating-point numbers, and the combined language subroutines are also used to perform floating-point addition, subtraction, multiplication and division. Compared with the CPU with floating-point hardware, the floating-point operation speed may be more than a hundred times slower.


step2:
It is easy to multiplication using an adder + shift operation, and it is also easy to divide using a subtractor + shift operation. Multiplication of floating point numbers is simpler than addition, and addition is more difficult than multiplication.


step3:
using "Multi-core + Hyper-Threading" can be use to multiply the computer speed
CPUs have a lot of computing cores that each have an ALU, a scratchpad, a control circuit, etc. Each core can execute instructions, so when they run at the fastest, four cores can achieve quadruple speed. 


step4:
The main advantages of DRAM include the following:

1.Its design is simple, only requiring one transistor.
2.The cost is low in comparison to alternative types of memory such as SRAM.
3.It provides higher density levels.
4.More data can be stored using DRAM.
5.Memory can be refreshed and deleted while a program is running.
