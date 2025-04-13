- 2's complement: reverse & +1
- BCD code (binary coded decimal): Rule to perform addition: (i) add 110 to the result if it is between 1010 and 1111 (9~15) (ii) add 110 to the result if there is a carry
- 

| ROM (read only memory):主要是只读（部分可改写，如 Flash ROM)                                                                                                                                                                          | RAM (random access memory):可读可写                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. ROM contains programs and information essential to operation of the computer.  <br> 2. for permanent data which cannot changed by the user<br>3. called as nonvolatile memory<br>4. Data does not lost when power off | 1. for temporary storage of programs that it is running<br>2. Data lost when power off<br>3. called as volatile memory <br>（4. 属于Read/Write Memory (R/W Memory)） |
| **Memory**                                                                                                                                                                                                               |                                                                                                                                                                  |

1. Address lines: Wires carry an address of a location being accessed. (unidirectional from external circuit from memory)
2. Data lines: Wires carry the data content being transferred between external circuit and memory (bidirectional)
3. Enable: a wire carries to a control signal to enable the memory chip. (unidirectional from external circuit to memory)
4. Read: a wire carries to a control signal to instruct the memory chip the operation is a read operation. (unidirectional from external circuit to memory)
5. Write: a wire carries to a control signal to instruct the memory chip the operation is a write operation. (unidirectional from external circuit to memory)

**Read a byte from a location**：
•External circuit sets the address of the location to address lines
•External circuit enables the chip enable
•External circuit enables Read
•The memory chip then puts the content of the selected location on D0-D7.
•Now extern circuit can access the data from D0-D7
**Write a byte to a location**
•External circuit sets the address of the location
•External circuit enables the chip
•External circuit puts the data on D0-D7
•External circuit enables the Write line
•The memory chip then saves incoming data on the corresponding location.

**Basic Computer Architecture**
-Computer: Perform a number of elementary computer operations (instructions) that manipulate information, called data.
-Instruction Set: The collection of all the instructions is called the instruction set of that computer.
-Program: Consists of a number of Instructions.
A digital computer may be divided into 3 different parts: The Central Processing Unit (CPU), The Memory, The Input/Output Devices (I/O)
**Computer**: Execute the programs by run the instructions one-by-one.
1.Load an instruction from memory to CPU.
2.Execute the instruction.
3.During the execution, the CPU may need to read or write the data from or to the memory.
**Input units**: Computer accepts information through input units, which read the data. (keyboard, mouse). Each input unit has some corresponding addresses.
**Memory**: Store programs and data. 
A program contain many instructions stored in memory. Each memory unit or location has an address.
Primary storage and secondary storage: Primary (IC chips in the computer) – to hold data and programs which are currently used; Secondary (disk) – to hold large amount of data or programs which are not currently used.
**Output units**: Counterpart of the input unit. Send processed results to the outside world. (monitor). Each output unit has some corresponding addresses.
**CPU (Central Processing Unit):** Inside a CPU, there are
• Arithmetic/logic unit (ALU): to perform the arithmetic and logic operation
• Control unit : coordinating the machine’s activities
• Registers : to store temporary data
In modern computer systems, 
• CPU, memory, and a number of device controllers are connected to the system bus.
• I/O devices and the CPU can execute concurrently.
• Each device controller is for a particular device type.
• Each device controller has a local buffer (a small number of registers).
• CPU moves data from/to main memory to/from the local buffers.
• I/O transfer is between the device and local buffer of controller.
• Device controller can inform CPU that it has finished its operation. (by using interrupt)

**Bus**
• CPU is connected to memory and I/O through strips of wire called a bus.
• Buses are used to Communicate between the computer components. – Data Bus – Address Bus – Control Bus
**The Operation of Bus**
• The CPU puts the address on the ***address bus***, and the decoding circuitry finds the device (decoding the address and then set a correct signal to the enable pin of the devices).
• The CPU uses the ***data bus*** either to get data from that device or to send data to it.
• The ***control buses*** are used to provide read or write signals.
• The address bus and data bus determine the capacity of a given CPU.

- CPU 通过 地址总线（Address Bus）选择 RAM 中的特定存储位置。
- 通过 数据总线（Data Bus）在 RAM 和 CPU 之间传输数据。
- 通过 控制总线（Control Bus）发送读/写等控制信号。
  **Data Bus**
  • Size of data buses is larger, the better the CPU is. (better processing power + more expensive) Example: 8 bits (slow), 16 bits, 32 bits, 64 bit (fast). An 8-bit data bus can send 1 byte a time. • Data buses are bi-directional.
  **Address Bus**
  • Size of address buses is larger, the larger the number of devices and memory locations that can be addresses. – Example: 8 bits (small), 16 bits, 32 bits, 64 bits (large). – A 16-bit address bus can indicate 216=64K addressable memory locations. – Regardless of the size of the data bus.
  • Address buses are unidirectional. (只能从 CPU 传输到 memory(内存) 或 I/O devices)
  • The number of address lines determines the number of locations with which a CPU can communicate.
  ✅ 读操作（Load）：  📤 CPU 发送地址 → 内存返回数据
  ✅ 写操作（Store）：  📤 CPU 发送地址 + 数据 → 内存存储数据

**Example CPU Read a byte from memory (read instructions or data item):**
•CPU puts the address (  ) of the location on address bus
•The decoding circuit selects the chip
•CPU sets the Read
•The memory chip then puts the content (  ) of the selected location (  ) on the data bus..
•CPU now can access the data.
•And then, … …
**Example CPU Write a byte to memory (write data item):**
• CPU puts the address of the location on address bus
• The decoding circuit (set the enable pin) selects the chip.
• CPU puts the data item one data bus.
• CPU sets the write signal.
• The memory chip then takes the data from the data bus and then saves it to the selected location (indicate by the address bus.
• And then …, …,
**Machine Clock:** 
• CPU performs the operations in the step-by-step manner.
• A CPU can be considered as a synchronic sequence logic circuit.
• Clock is used to synchronize work of the components on the machine.
• Clock Rate decides the performance of the computer.

**Inside CPU:**
• Accumulator and General Purpose Registers
– Accumulator (WREG) (注：Accumulator (累加器），在许多微控制器 (如 PIC 微控制器) 中被称为 WREG (Working Register，工作寄存器）)
– Registers
• Special-purpose registers
– Program Counter (PC) 
– Instruction Register (IR) 
– Stack Pointer 
– Status Word Register
– In PIC18, there are Bank and File Select Registers 
***bank select register:*** select which data space in RAM is active 
***file select register:*** for indirect addressing.
• Stack Point permits “context switching” in interrupt service routines (ISR) and subroutines

**Accumulator (WREG):**
A register stores the results of arithmetic and logic operation.
**Data Registers and Address Registers:**
stores data (variables) or addresses (addresses of variables).
**Program Counter (PC):** (see P.106 in this chapter)
– Store the address of the instruction to be executed in the next instruction cycles.
– Update automatically after CPU fetchs an instruction.
– PC is crucial for the control flow of a program and is responsible for ensuring that instructions are executed in the correct order.
**Instruction Register (IR):**
Store the instruction currently being executed or decoded
**Stack Pointer**
Help the implementation of a stack data structure.
**Status Word**
– Contain several bits.
– Each bit indicates the states of CPU.
– For example, a Carry flag indicates if the last addition operation produces a carry or not.

**Stack:**
• Stack：a section of RAM to store data items
• Stack register (stack pointer): point to the location of the top of the stack.
• Two operations on the stack：
– PUSH：put an item onto the top of the stack
– POP：remove an item from the top of the stack

| Assembly Language                                                                                                                                                                                       | High-Level Languages (BASIC, C, C++...)                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| machine instructions represented in mnemonics<br>• Has one-to-one correspondence with machine instructions<br>• Efficient in execution and use of memory; machine-specific and not easy to troubleshoot | Written in statements of spoken languages<br>• machine independent<br>• easy to write and troubleshoot<br>• requires large memory and less efficient in execution |

**The Machine Cycle**（1/2）
Every instruction in memory is executed by three
steps: ***Fetch -> Decode -> Execute***
• Each instruction has its micro-instruction ~~(or micro-operations). (A micro-operation is an elementary operation that can be performed in parallel during one clock pulse period.)~~
• The instruction decoder is to interpret the instruction fetched into the CPU.
**The Machine Cycle**（2/2）page.102 (a picture,cannot copy and paste)

---

# Chapter 1The PIC18 Microcontroller

**1. Harvard vs von Neumann Architecture**
| von Neumann | Harvard |
|--|--|
| uses the same address and data bus for code ROM space and data RAM space. | uses different address and data buses to access code ROM space and data RAM space. |
| is slow because ROM and RAM cannot be accessed simultaneously. | is easy for pipeline implementation and faster but expensive to implement and needs a lot of wires. |

**2. microprocessors and microcontrollers**
**General-purpose microprocessor:**
• CPU for Computers 
• No RAM, ROM, I/O, CPU on chip itself 
• Example：Intel’s x86, Motorola’s 680x0

**Microcontroller Unit (MCU) or micropcomputer unit:** 
An integrated electronic computing device that includes 3 major components on a single chip: Microprocessor (MPU), Memory, I/O (Input/Output) ports.

**Microcontroller:** 
• A smaller computer
• On-chip RAM, ROM, I/O ports...
• Example：Motorola’s 6811, Intel’s 8051, Zilog’s Z8 and PIC 18

• Support Devices (peripheral) 支持外设设备: device attached to a computer like Timers (counting number of pulses), A/D converter (Analog to Digital), Serial I/O (for example keyboard to main board)
• All components connected by common communication lines called the system bus. 所有的这些外设设备都通过公共通信线“系统总线”互联并与微控制器核心 (CPU) 通信 (“系统总线”包含地址总线、数据总线、控制总线，用来在 CPU 和外设之间传递指令、数据及控制信号)
|Microprocessor 微处理器| Microcontroller 微控制器 |
|--|--|
| • CPU is stand-alone, RAM, ROM, I/O, timer are separate. <br>只包含 CPU 或极少量缓存，外部需扩展 RAM、ROM、I/O 等<br>• Designer can decide on the amount of ROM, RAM and I/O ports<br>外设可灵活组合,可扩展性好<br>• General-purpose<br>• Expensive | • CPU, RAM, ROM, I/O and timer are all on a single chip.<br>• Fix amount of on-chip ROM, RAM, I/O ports<br>• For applications in which cost, power and space are critical<br>• Single-purpose<br>• Cheap |

**3. Embedded System**
– Operations managed behind the scenes by a microcontroller or microprocessor
– Operation System is designed for the application, not general purpose
– Example: fan, fax machine, photocopy machine, mouse
即，嵌入式系统是一种在特定设备或环境中“隐藏”运行、具有专用操作系统或固件的微控制器/微处理器系统，常见于各类日常和工业电子产品中。
• Embedded system means the processor is embedded into that application.
• An embedded product uses a microprocessor or microcontroller to do specified tasks only.
• In an embedded system, there is only one application software that is typically burned into ROM.
• Some embedded products using microcontrollers. Example：printer, keyboard, video game player, door opener, copier, ABS, fax machine, camera, cellular phone, keyless entry, microwave...

Processors in Embedded Systems: 
Choice for an embedded product: microcontroller:
1.cost down 2.embedded processor ＝ microcontroller 3.In future, an entire computer on a chip 4.high-end embedded systems may use microprocessors
Three criteria in Choosing a Microcontroller:
1.meeting the computing needs of the task efficiently and cost effectively
• speed, the amount of ROM and RAM, the number of I/O ports and timers, size, packaging, power consumption • easy to upgrade • cost per unit
2.availability of software development tools • assemblers, debuggers, C compilers, emulator, simulator, technical support
3.wide availability and reliable sources of the microcontrollers.

### 4.Overview of PIC18

**Basic Data Format (8-bit) in PIC18**

1. Signed Integers: Seven bits (Bit6 to Bit0) represent the magnitude of a number.
   – The eighth bit (Bit7) represents the sign of a number.
   – Positive numbers: 00 to 7F (0 to 127) ; Negative numbers: 80 to FF (-1 to -128) (in 2’s complement)
2. American Standard Code for Information Interchange (ASCII)
   – Seven-bit alphanumeric code with 128 combinations (00 to 7F)
   注：虽然 ASCII 本质是 7 位，但在 8 位微控制器如 PIC18 中通常会用一个完整的字节 (8 位) 来存储，最高位保持为 0.
3. Unsigned Integers: All eight bits (Bit7 to Bit0) represent the magnitude: Range 00 to FF in Hex and 0 to 255 in decimal
4. Binary Coded Decimal Numbers (BCD)
   – Example: 0010 0101 represents the binary coding of the decimal number 25 which is different in value from 25H.

**PIC18F Microcontroller Families**
PIC microcontrollers are designed using the Harvard Architecture which includes:
– Microprocessor unit (MPU)
– Program memory for instructions
– Data memory for data
– I/O ports
– Support devices such as timers

| two set of buses                                   |                     |
| -------------------------------------------------- | ------------------- |
| program address-> (21-bit) <br>data   <-> (16-bit) | Program Memory (PM) |
| address -> (12-bit)<br>data    <-> (8-bit)         | Data Memory         |
| 程序总线：用来从程序存储器（PM）中读取指令（Program）                    |                     |
| 数据总线：用来对数据存储器（Data Memory）进行读写操作                   |                     |

**Microprocessor Unit**
Includes Arithmetic Logic Unit (ALU), Registers, and
Control Unit
• Arithmetic Logic Unit (ALU)
• Instruction decoder
• Status register that stores flags 5-bit
• WREG – working register, 8-bit accumulator

• **Program Counter (PC)**
o 21-bit register
o Store the address of the instruction to be executed in the next instruction cycles.
o Update automatically after CPU fetchs an instruction.
o Responsible for ensuring that instructions are executed in the correct order.

• **Bank Select Register (BSR)**
4-bit register used in direct addressing the data memory
• **File Select Registers (FSRs)**
12-bit registers used as memory pointers in indirect addressing data memory
• **Control unit**
Provides timing and control signals to various Read and Write operations

**PIC18F - Address Buses:**
• Address bus
– 21-bit address bus for [program memory addressing]
capacity: 2 MB of memory (because 2^21^)
– 12-bit address bus for [data memory addressing] capacity: 4
KB of memory
**Data Bus and Control Signals:**
• Data bus
– 16-bit instruction/data bus for [program memory]
– 8-bit data bus for [data memory]
• Control signals
– Read and Write

**PIC18F452/4520 Memory**
• Program Memory: 32 K
– Address range: 000000 to 007FFFH (剩下的: Unused Memory Space Read '00')
• Data Memory: 4 K
– Address range: 000 to FFFH
• Data EEPROM
– Not part of the data memory space
– Addressed through special function registers

PIC18F452/4520 – Data Memory with **Access Banks**

1. 每个 Bank 都是一段独立的 RAM 存储区域。
   2. 使用 BSR（Bank Select Register） 来切换 Bank:
      BSR（银行选择寄存器）存储了当前访问的 Bank 编号，如果要访问不同的 Bank，。
2. 在 PIC18 微控制器里，RAM（存储器）被分成多个 Bank（存储块），每个 Bank 有固定大小的地址空间，但是 CPU 一次只能访问当前选中的 Bank。
   假设你要访问不同 Bank 里的变量，每次都要先修改 BSR 的值来切换 Bank，否则 CPU 会找不到正确的数据。这个切换过程需要额外的指令，会拖慢程序的运行速度。
   为了减少这种切换 Bank的麻烦，PIC18 提供了一个特殊的区域，叫 Access Bank，让程序可以随时访问其中的变量，而不需要切换 Bank。
   想象一下：
   •普通 Bank就像多层文件柜，每次要查找不同层的文件时，都得先调整抽屉的位置（切换 Bank）。
   •Access Bank就像是随手可拿的文件夹，最常用的资料都放在这里，随时可以拿到，不需要调整抽屉。
3. Access Bank 如何工作？
   在 PIC18 里，Access Bank  **固定**分配了一部分内存：
   •前 96 个字节  →  特殊功能寄存器（SFRs），比如控制 GPIO、定时器的寄存器。
   •后 160 个字节  →  普通 RAM 变量（GPRs），可以存放程序里最常用的数据。
   只要把变量放到 Access Bank 里，就可以直接访问，不需要先切换 Bank。

**PIC18F452 I/O Ports**
• Five I/O ports
– Digital IO is the most fundamental mode of connecting a MCU to external world. The interface is done using what is called a PORT.
– The IO ports can be programmed as input or output.
– PORT A, B, C, D, E
– Most I/O pins are multiplexed
– Generally have eight I/O pins with a few exceptions
– Addresses already assigned to these ports in the design stage
– Each port is identified by its assigned SFR

**MCU Support Devices** (略）page.36
**PIC18F Special Features** (略）page.38
**PIC18F Instructions and Assembly Language:** 
• Has 77 instructions. Earlier PIC family of microcontrollers have either 33 or 35 instructions.
• In PIC18F instruction set, all instructions are 16-bit word length except four instructions that are 32-bit length.

**MOVLW**（Move Literal to WREG）用于将字面值（Literal）加载到 WREG（工作寄存器）。
**MOVWF**（Move WREG to File Register）的作用是将 WREG（工作寄存器）中的数据存入指定的文件寄存器（F）。
**TRIS:** TRISA/B/C/D/E are to control Input/Output of port
如何设置 TRIS: 写 1 → 对应PORT配置为输入模式 ; 写 0 → 对应PORT配置为输出模式

```
example:
MOVLW 00    ; 将 W 寄存器加载 0 //`00`被写入`TRISC`,意味着 PORTC 的所有位都被设为输出模式
MOVWF TRISC,0   ; 将 W 寄存器的值（00）写入 TRISC，设置 PORTC 为输出
MOVLW 0x55    ; 将 0x55 赋值给 W  // 0x55 在二进制中是 `0101 0101`（交替的 0 和 1）
MOVWF PORTC,0   ; 将 W（0x55）写入 PORTC，点亮交替 LED // 0x55(0101 0101)写入`PORTC`后: 0位:LED亮, 1位:LED灭,...
```

---

# Chapter 2 The PIC18 Assembly Language Programming

> 2.1 Inside the PIC18
> 2.2 Simple PIC18 Program
> 2.3 Introduction to PIC18 Assembly Programming
> 2.4 Assembling and Running an PIC18 Program
> 2.5 The Program Counter and ROM Space in the PIC18
> 2.6 RISC Architecture in the PIC
> 2.7 PIC18 Flag Bits and the PSW Register
> 2.8 PIC18 Register Banks and Stack

Review: PIC18 Architecture
• Harvard Architecture which includes: 1.Microprocessor unit (MPU) 2.Program memory for instructions 3.Data memory for data 4.I/O ports 5.Support devices such as timers
Review: PIC18 Memory Organization
• Program Memory
– 21-bit address bus
– Address up to 2^21^=2M bytes of memory
– Not all memory locations are implemented
– 16-bit data bus
• Data Memory
– 12-bit address bus (4k bytes memory space)
– 8-bit data bus

**Banks in Data Memory**
• Divided into 16 banks.
• 256 bytes per bank
• Access (Default) Bank is a 256-byte bank consisting of:
– 128 bytes of GPRs located at 00H to 7FH in the access bank, mapped from 000H to 07FH of the data memory
– 128 bytes of SFRs located at 80H to FFH in the access bank, mapped from F80H to FFFH of the data memory
• A program that requires more than the amount of RAM provided in the access bank necessitates bank switching.
PIC18 uses the bank concept because in many instructions there are 8 bits to indicate the RAM address (12 bits address)

**General-purpose and Special-function registers:**
• Two types of registers: general-purpose (GPR) and special-function registers (SFR)
• GPRs provide storage for variables used in a program.
• SFRs are used to control the operation of the CPU and peripherals.
 1.The WREG register is involved in the execution of many instructions.
 2.The STATUS register contains the arithmetic status of the ALU
 3.TRISx

**Stack pointer**
Stack Pointer是 5 位 => 0~31=2^5^, however, if 0 0000 then empty, 所以实际只有31 locations (31层碟子) , 每层是21 bits each (地址的长度)

**PIC18F Programming Model**
Divided into 2 groups：
• Arithmetic Logic Unit (ALU) and Registers
 – From Microprocessor Unit (MPU)
• Special Function Registers (SFRs)
 – From Data (File) Memory 
 **Registers**
1.Program Counter (***PC***) – 21-bit register functions as a pointer to program memory during program execution
2. ***STATUS***: Flag Register – 5 individual bits called flags
3. WREG (***W***): Working Register – 8-bit Accumulator
4. Product Register – 16-bit Product of 8-bit by 8-bit Multiply
5. Table Pointer (access program ROM) – 21-bit register used as a memory pointer to copy bytes between program memory and data registers
6. Stack Pointer (***SP***) – 5-bit register used to point to the stack
7. ***Stack*** – 31 registers used for temporary storage of memory addresses during execution of a program
8. **BSR: Bank Select Register** 
• 4-bit Register 
• Provides upper 4-bits of 12-bit address of data memory
9. **FSR: File Select Registers** 
• FSR0, FSR1, and FSR2 
• FSR: composed of two 8-bit registers FSRH and FSRL
• Used as pointers for data registers
• Holds 12-bit address of data register
| 直接寻址（Banked or Access） | 间接寻址（使用 FSR） |
|--|--|
| • 如果使用 Access Bank（a=0，访问“Access”区），则只需 8 位地址即可访问 Access Bank 的 256 字节。<br>• 如果使用 Banked 模式 (a=1)，则需要在指令里指定 8 位偏移，同时由 BSR 提供 4 位 Bank 号，共 12 位来访问全局的任何 Bank。 | • 先把目标地址（12 位）写入 FSR，然后通过 `INDFx` (Indirect File Register) 来访问 FSR 所指向的内存位置。<br>• 这种方式不受 BSR 的限制，可灵活地在程序中修改 FSR 以指向任意 Bank 的任意地址。 |

**Flags in Status Register**
• N (Negative Flag) – Set when bit B7 is one as the result of an arithmetic/logic operation
• OV (Overflow Flag) – Set when result of an operation of signed numbers goes beyond 7-bits
• Z (Zero Flag) – Set when result of an operation is zero
• DC (Digit Carry Flag) (Half Carry) – Set when carry generated from Bit3 to Bit4 in an arithmetic operation
• C (Carry Flag) – Set when an addition generates a carry

**Special Function Registers (SFRs):** Data registers associated with I/O ports, support devices, and processes of data transfer
• I/O Ports (A to E) • Interrupts • EEPROM • Serial I/O • Timers • Capture/Compare/PWM (CCP) • Analog-to-Digital (A/D) Converter

Data Format Representation: Data can only be represented as **an 8-bit number** in PIC18
• Four ways to represent a byte: Hexadecimal (Default), Binary, Decimal, ASCII.
1.**Hexadecimal Numbers:** 4 ways to represent:
a) movlw 99 (Hex is the default representation)
b) movlw 99H or movlw 99h
c) movlw 0x99
d) movlw h ‘99’
注: If a) or b) is used and the starting hex digit is A-F, the number must be perceded by a 0. – e.g., *movlw C6 is invalid*. Must be movlw 0C6.
**Binary:** The only way to represent a binary number is to put a B (or b) in front: movlw B ‘10011001’
**Decimal:** 2 ways to represent:
(a) Put a D (or d) in front: movlw D ‘12’  (b) Use the “.value” format: movlw .12
**ASCII character:** The only way to represent an ASCII character is to put a A (or a) in front: movlw A ‘2’.
• The ASCII code 0x32 is used to represent the character ‘2’. 0x32 is stored in WREG. 即, 在 ASCII 中，字符 '2' 的代码是 0x32。当你将 '2' 存入 WREG 时，实际存的是 0x32。虽然 PIC 不会自动把 0x32 识别为 ASCII，但当它用于显示、字符串存储或传输时，就会按 ASCII 解释为 '2'。

**PIC18 Instruction Set:** 
• Includes 77 instructions: 73 one word (16-bit) long & 4 two words (32-bit) long
• Divided into seven groups: Move (Data Copy) and Load, Arithmetic, Logic, Program Redirection (Branch/Jump), Bit Manipulation, Table Read/Write, Machine Control

**The WREG register (accumulator)**
• One of many registers for arithmetic and logic operation.
•  8-bit register => any data larger than 8 bits must be broken into 8-bits chunks before it is processed

**MOVLW** : Move 8-bit data into WREG => 将 8 位的字面值 (literal value) 加载到 WREG 寄存器中,超过8 bits不行
**ADDLW** k; Add literal value k to WREG (k +WREG)  Eg: 
MOVLW 12H; => WREG: 0001 0010
ADDLW 16H; => WREG: 0010 1000

**The PIC File register (data memory)**
• 2 parts: General Purpose Register (GPR) and Special Function Register (SFR)
注：在 PIC ，“File Register” 指的就是整个 数据存储器 (Data Memory) 空间，用来表示可由指令直接或间接访问的所有寄存器地址范围，包括：
• 通用寄存器（GPR）：存放程序运行时的普通数据或变量/8-bit registers
• 特殊功能寄存器（SFR）：用于控制和配置 MCU 的各种硬件功能used for control of the microcontroller or peripheral/dedicated to specific functions such as ALU status, timers, serial communication, I/O ports, ADC,…/8-bit registers
(Their numbers varies from one chip to another)

**File Registers and bank in the PIC18**
• The PIC18 Family can have a maximum of 4096 Bytes for File Registers
• The File Registers has addresses of **000- FFFH** (2^12^)
• Divided into 16 **256-byte banks** (16 $\times$ 256=4096) : Divided into 2 equal discontinuous sections (each 128 Bytes).
 – GP RAM, from 099H to 07FH
 – SFR, from F80H to FFFH
• At a time only one of 16 banks is used. Bank switching is a method used to access all the banks. 
• There is one logical bank (access bank). `eg: MOVWF 0x20, ACCESS`
**Why we need the bank concept ?**
• In PIC18, there are 4096 file registers (4096 locations) => We need a 12 bits address to refer a register
• In PIC18, many instructions are with 2 bytes length only. One byte is usually for specifying the operation. Another byte is usually for specifying the data or the data address.
• We usually only have 8 bits to specify a location.
• With the bank concept, we use the mentioned 8 bits to refer a location in a bank. Another higher order 4 bits address is stored in bank selection register (BSR)

**Using instructions with the default access bank**
Instructions to access other locations in the file register for ALU and other operations. 即, 这些指令可以在文件寄存器  (File Register) 的不同位置之间进行读写，用于执行算术逻辑运算 (ALU操作 (Arithmetic Logic Unit))或其他相关操作

| Instruction                                                                                                                                   | function                                                                                                                       | assembly form                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| MOVWF                                                                                                                                         | MOVE  WREG -> a location：将 WREG 的内容复制到文件寄存器。                                                                                   | ` MOVWF f, a`                                                                                                        |
| COMF                                                                                                                                          | 对寄存器内容取反。                                                                                                                      | `COMF f, d, a`                                                                                                       |
| DECF                                                                                                                                          | Decrement File, 寄存器内容减 1。与INCF相对。                                                                                              | `DECF f, d, a`                                                                                                       |
| MOVF                                                                                                                                          | MOVE the content of a location to-> W：将File Reg Address移动到 WREG。                                                               | `MOVF f, d, a`<br>`MOVF 0x40, 0, 0; 将地址 0x40 的内容读取到 WREG`                                                            |
| MOVFF                                                                                                                                         | MOVE the content of a location to another location：在文件寄存器之间传输数据（4 bytes instruction）。Move File to File是一个 4 字节指令，用于在RAM内部移动数据。 | `MOVFF src, dest`<br>`MOVFF PORTB, PORTC; 将 PORTB 的内容复制到 PORTC`<br>`MOVFF 0x100, 0x120; 将 0x100 地址处的数据复制到 0x120 地址处` |
| 注:  `f`：文件寄存器地址。                                                                                                                              |                                                                                                                                |                                                                                                                      |
| `d`：  `d=0` → 结果写入 WREG（copies the content of fileReg (from I/O pin) to WREG）; `d=1` → 结果写回 `f` (文件寄存器的内容保持不变, 但可能will affect the status Reg) |                                                                                                                                |                                                                                                                      |
| `a`：访问方式；`a=0` 访问 Access Bank，`a=1` 使用 BSR 选择的 Bank（有时用 `ACCESS` / `BANKED` 关键字替代）                                                            |                                                                                                                                |                                                                                                                      |
| `src`：源文件寄存器地址（可为 12 位地址）。                                                                                                                    |                                                                                                                                |                                                                                                                      |
| `dest`：目的文件寄存器地址（可为 12 位地址）。                                                                                                                  |                                                                                                                                |                                                                                                                      |

**ORG start-address**
Eg: ORG 0200H ;put the following codes start at location 200H
**EQU and SET Directives**
EQU 等价指令 – associates a constant number with an address label. Eg: 

```
COUNT equ 0x25; -> defined a label for a constant (defined a location/address in RAM)
...........
movlw COUNT;  WREG=0x25 (将 0x25 载入 WREG)
```

SET 可变指令 – identical to EQU, but value assigned by SET can be reassigned later. Eg:

```
COUNT set 0x00; COUNT 先设为 0x00，
...........
COUNT set 0x25; 然后又被修改为 0x25，这在 EQU 中是无法做到的。
```

**CBLOCK Directive**
`CBLOCK`（“Contiguous Block”）是一种用来**为变量分配连续地址**（或指定地址）的汇编指令。它会从指定的起始地址开始，将后续列出的标签逐一分配到连续的内存单元中，直到遇到 `ENDC` 结束。
也可以在标签后面用 “=`<地址/表达式>`” 的方式人为指定某个标签的确切地址，从而在地址分配中产生“跳跃”。

```
CBLOCK 0x50
   test1, test2, test3, test4
ENDC
```

• 含义：从地址 `0x50` 开始，顺次分配给 `test1`、`test2`、`test3`、`test4`。
• 最终结果：  `test1 = 0x50`  `test2 = 0x51`   `test3 = 0x52`  `test4 = 0x53`

**Instruction size of the PIC18:** 2-Byte or 4-Byte
• 2 字节指令：大多数普通指令（如 `MOVWF`, `COMF`, `DECF`, `MOVF` 等）只需要 16 位就能表达操作码和少量地址/操作数
• 4 字节指令：当需要更大地址字段或双地址字段（如 MOVFF 源地址+目的地址，或 GOTO/CALL 的程序地址），就会扩展成 4 字节. Eg:

```
MOVFF fs, fd
; `fs`（Source File Register）：源寄存器地址（12-bit）
; `fd`（Destination File Register）：目标寄存器地址（12-bit）
1100 ssss ssss ssss  ; 12-bit 源地址 (fs)
1111 dddd dddd dddd  ; 12-bit 目标地址 (fd)
```

```
GOTO k; `k` 是 21-bit 目标地址
1110 1111 k₇ kkkk kkkk₀  ; 高 11 位（bit 20~10）
1111 k₁₉ kkkk kkkk kkkk₈  ; 低 10 位（bit 9~0）
```

**PIC18 Microcontroller Stack**
• **Hardware Stack**  – 31 registers – 21-bits wide – Not part of program memory or data registers
• Stack Pointer (STKPTR) – 5-bit address
• Top of the Stack (TOS) – Pointed to by the stack pointer 
– Copied into 3 special function registers: TOSU (Upper), TOSH (High), and TOSL (Low)

注：**Hardware Stack** (硬件堆栈) 用于存放**子程序或中断**返回地址。
**Stack Pointer Register**是一个**专门的寄存器**，用来记录当前堆栈指针位置以及是否出现堆栈溢出（Overflow）或 堆栈下溢（Underflow）等异常。
1.**SP4:SP0**（位 4-0）：这 5 位共同表示当前的硬件堆栈指针（Stack Pointer）的索引，可取值 0~31，因此 PIC18 的硬件堆栈最多可存放 31 个返回地址
2. **STKOF（B7）**：当堆栈已满（已经使用了 31 个层级）却仍尝试执行 `CALL` 或新的中断压栈时，就会触发**Stack Overflow**。这个标志位会被硬件置 1，表示溢出状态。
3. **STKUNF（B6）**：当堆栈已空（SP4:SP0 = 0）却仍尝试执行 `RETURN` 或 `RETFIE` 弹栈时，就会触发**Stack Underflow**。这个标志位会被硬件置 1，表示下溢状态。

`CALL` 指令会将“**下一条**指令的地址”压入堆栈并使堆栈指针递增 (**注意是CALL行的下一条**），而
`RETURN` 指令则从堆栈弹出返回地址并使堆栈指针递减。
`GOTO` 则不使用堆栈。

---

## Chapter 3 Branch Loop, and IO Port

> 3.1 Loop and Jump Instructions
> 3.2 IO PORT
> 3.3 Time Delay Generation and Calculation

2 unconditional jumps：
**`GOTO`**（a 4-byte instruction，Long Jump）（advantage: can goto anywhere you like; disadvantage: program size become larger）
**`BRA`**（a 2-byte instruction，Short Jump）

**Loop in PIC** : 2 ways to do looping
• Using DECFSZ instruction (fullname: Decrement File Register, Skip if Zero)
• Using BNZ\BZ instructions
**DECFSZ**：减 1 后若结果为 0，就“跳过”下一条指令；典型用法是计数循环。eg:

```
Loop:
    DECFSZ   COUNTER, F   ; COUNTER = COUNTER - 1，若结果为0则跳过下一条
    GOTO     Loop         ; 如果COUNTER != 0，就继续循环
    ; 如果COUNTER == 0，则跳过GOTO，执行后续指令
```

**BZ/BNZ/BNC**：依赖 STATUS 寄存器中的标志位（Zero、Carry 等）进行分支跳转。
**BZ**：Jump if previous result is 0（W=0）
**BNZ**：Jump if previous is not zero（W!=0）
**BNC**：Jump if no carry（CY=0）

**CALL and RCALL**
• CALL: 4 bytes；Call a subroutine in anywhere；format is similar to GOTO
• RCALL: 2 bytes；Call a subroutine who address should be within Similar to
BRA；Relative address

**Machine Cycle**：In PIC18, 4 clock cycles=1 machine cycle (MC在时间上是4倍, 在频率上是1/4)

**Relative Address Calculation in conditional brances Instructions**
BNC N_1
偏移量计算: (BNC指令的下一行地址 $-$ N_1行地址)/2（注意：16进制和10进制的问题）
