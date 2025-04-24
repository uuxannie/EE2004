# miniproject_final
```asm
LIST P=18F4520
#include <P18F4520.INC>
CONFIG OSC = XT    
CONFIG WDT = OFF   
CONFIG LVP = OFF  
CBLOCK 0x20
digit0      
digit1       
digit2       
digit3 
countL       
countH      
inputL       
inputH       
int0_flag
temp1
temp2
input       
cycle_num
Result
n
n0
ENDC

ORG 0x0000
    GOTO MAIN

ORG 0x0008
    BTFSC INTCON, INT0IF
    CALL INT0_ISR
    RETFIE

ORG 0x0100
MAIN:
    MOVLW 0x0F          
    MOVWF ADCON1
    CLRF TRISD        
    CLRF PORTD          
    CLRF TRISC            
    CLRF PORTC            
    SETF TRISB       
    CLRF countL       
    CLRF countH
    BCF INTCON, INT0IF
    BSF INTCON, INT0IE
    BCF INTCON2, INTEDG0
    BCF INTCON3,INT1IF
    BSF INTCON3,INT1IE
    BCF INTCON2,INTEDG1
    BCF INTCON3,INT2IF
    BSF INTCON3,INT2IE
    BCF INTCON2,INTEDG2
    BSF INTCON, GIE     

LOOP:
    MOVFF countL, inputL
    MOVFF countH, inputH
    CALL bin_to_bcd     
    CALL scan_display   
    GOTO LOOP

INT0_ISR:
    movlw 0x01
    addwf countL, F
    BTFSC STATUS, C
    addwf countH, F
    movlw 0x01
    movwf int0_flag
    BCF INTCON, INT0IF
    RETURN

INT1_ISR:
    MOVLW 7         
    SUBWF countL, W  
    BTFSS STATUS, Z  
    GOTO  calc_factorial
    GOTO  Else
calc_factorial:
    MOVLW 1      
    MOVWF inputL     
    MOVLW 0        
    MOVWF inputH    
    MOVFF countL, n 
    MOVF  n, W      
    BEQ Done  

FactorialLoop:
    MOVF n, W       ; 将 n 的值加载到 WREG
    MOVWF n0        ; 备份 n
    MOVF Result, W  ; 将当前结果加载到 WREG
    MULWF n0, W     ; 计算结果 * n
    MOVWF Result    ; 将新结果存储回 Result
    DECFSZ n, F     ; n = n - 1
    GOTO FactorialLoop

Done:
    CALL bin_to_bcd     
    CALL scan_display   

Else:
    NOP

INT2_ISR:
    clrf countL
    clrf countH
    clrf digit0
    clrf digit1
    clrf digit2
    clrf digit3
    clrf int0_flag
    BCF INTCON3, INT2IF
    RETURN

delay:
    MOVLW D'1000'
    MOVWF temp1
delay_outer:
    MOVLW D'200'
    MOVWF temp2
delay_inner:
    NOP
    NOP
    DECFSZ temp2, F
    GOTO delay_inner
    DECFSZ temp1, F
    GOTO delay_outer
    RETURN

bcd_7seg: 
    movlw low bcd_table
    movwf TBLPTRL
    movlw high bcd_table
    movwf TBLPTRH
    movlw upper bcd_table
    movwf TBLPTRU
    movf  input, W
    addwf TBLPTRL, F
    movlw 0
    addwfc TBLPTRH
    addwfc TBLPTRU
    tblrd*
    movf TABLAT, W
    return

bcd_table:
    db 0x3F,0x06,0x5B,0x4F,0x66,0x6D,0x7D,0x07,0x7F,0x6F


bin_to_bcd:   ; Double Dabble Algorithm (Shift-and-Add-3)
    clrf    digit0
    clrf    digit1
    clrf    digit2
    clrf    digit3
    movlw   .16
    movwf   cycle_num

convert_loop:
    movf    digit0, w
    sublw   .5  
    BTFSS   STATUS,Z
    goto    noadd0
    movlw   .3
    addwf   digit0, F
noadd0:
    movf    digit1, w
    sublw   .5  
    BTFSS   STATUS,Z
    goto    noadd1
    movlw   .3
    addwf   digit1, F
noadd1:
    movf    digit2, w
    sublw   .5  
    BTFSS   STATUS,Z
    goto    noadd2
    movlw   .3
    addwf   digit2, F
noadd2:
    movf    digit3, w
    sublw   .5  
    BTFSS   STATUS,Z
    goto    noadd3
    movlw   .3
    addwf   digit3, F
noadd3:
    rlcf     inputL, F
    rlcf     inputH, F
    rlcf     digit0, F
    rlcf     digit1, F
    rlcf     digit2, F
    rlcf     digit3, F
    decfsz  cycle_num, F
    goto    convert_loop
    return


scan_display:
    movf    digit0, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x00
    movwf   PORTC
    call    delay_display

    movf    digit1, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x01
    movwf   PORTC
    call    delay_display

    movf    digit2, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x02
    movwf   PORTC
    call    delay_display

    movf    digit3, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x03
    movwf   PORTC
    call    delay_display
    return

delay_display:
    movlw   D'50'
    movwf   temp1
wait_loop:
    nop
    nop
    decfsz  temp1, F
    goto    wait_loop
    return

    END
```

# Asg 6 INT example

当然可以！你这段代码是写给 **PIC18F4520** 单片机的汇编程序。它的主要功能是：

> **使用外部中断 INT0 触发事件来累加一个变量，并把它的值显示在 PORTD。**

---

## 🧩 结构总览

这个程序可以分为几个主要部分：

1. **设置系统参数（晶振、看门狗等）**
2. **中断向量初始化**
3. **主程序初始化与循环**
4. **INT0 外部中断服务程序**
5. **软件延时子程序**

---

## 🔍 分段详细讲解

---

### ✅ 1. 配置与初始化部分：

```asm
LIST P=18F4520
#include <P18F4520.INC>

CONFIG OSC = XT       ; 使用XT晶振（4–8MHz）
CONFIG WDT = OFF      ; 关闭看门狗定时器
CONFIG LVP = OFF      ; 禁用低电压编程（LVP）

ORG 0000H
GOTO MAIN             ; 上电或复位后跳转到 MAIN

ORG 0008H             ; 外部中断0 的中断向量地址
BTFSC INTCON,INT0IF   ; 如果 INT0 中断标志位为1
CALL INT0_ISR         ; 进入中断服务程序
RETFIE                ; 从中断返回（恢复状态）
```

---

### ✅ 2. 主程序 `MAIN`

```asm
ORG 00100H
MAIN
MOVLW 0x0F
MOVWF ADCON1         ; 配置 AN0~AN3 为数字输入（关闭模拟功能）

SETF TRISB           ; 设置 PORTB 全部为输入（包括 INT0 = RB0）
CLRF TRISD           ; 设置 PORTD 为输出

BCF INTCON,INT0IF    ; 清除 INT0 的中断标志位
BSF INTCON,INT0IE    ; 使能 INT0 中断
BCF INTCON2,INTEDG0  ; 设置 INT0 在“下降沿”触发中断
BSF INTCON, GIE      ; 全局中断使能
```

---

### ✅ 初始化一个变量 & 显示：

```asm
MOVLW 0xFF
MOVWF 0              ; 把0xFF写入寄存器0（通用RAM地址0）
MOVFF 0, PORTD       ; 把寄存器0的值显示在PORTD
```

---

### ✅ 主循环 `OVER`：

```asm
OVER
MOVFF 0, PORTD       ; 持续显示寄存器0的值到PORTD
BRA OVER             ; 死循环
```

---

### ✅ INT0 中断服务程序：

```asm
INT0_ISR
INCF 0, F            ; 寄存器0中的值加1
CALL delay           ; 延时（防抖或节奏控制）
BCF INTCON,INT0IF    ; 清除中断标志
RETURN
```

---

### ✅ 延时子程序 `delay`：

```asm
delay:
MOVLW D'100'
MOVWF 1              ; 外层循环次数 = 100
back:
MOVLW D'0'
MOVWF 2              ; 内层循环次数 = 0

here:
NOP                  ; 占位操作，耗时
NOP
NOP
NOP
NOP
NOP
NOP
DECF 2, F
BNZ here             ; 内层循环
DECF 1, F
BNZ back             ; 外层循环
RETURN
```

这个延时是一个双层循环，简单制造时间延迟，防止中断频繁或防抖处理。

---

## 📌 总结一下功能：

| 模块   | 功能描述                  |
| ---- | --------------------- |
| 中断配置 | 启用 INT0 外部中断，下降沿触发    |
| 主程序  | 设置端口方向，将变量的值显示到 PORTD |
| 中断响应 | 每次外部中断触发时将变量自增，并延时    |
| 显示   | 将变量通过 PORTD 实时输出      |
| 变量存储 | 变量存在地址 0 的寄存器中        |

---

## 🧠 举个例子：

假如你用个按钮接到 RB0（INT0）上，每按一次按钮就会触发中断，变量就加一，PORTD 的值就变化一次。你可以用 LED 接到 PORTD 来观察数值变化。

---

如果你有硬件电路图，或者想要扩展功能（比如多键输入、用 LCD 显示等），我也可以帮你！

# mini project 思路：

以counter为基底，把从1数到7换成从1!(=1)数到7!(=5040)。阶乘的结果不使用查表法，使用loop。在4*7segment显示结果时，另外需要一些代码。

实现该思路：

1 先写出一个最简单的counter，结果能用一位显示。

2 升级版counter，能显示4位的counter。（0-9999）（即实现思路的最后一部分）

3 写出计算阶乘的loop

## 1

```asm
LIST P=18F4520
#include <P18F4520.INC>

CONFIG OSC = XT    
CONFIG WDT = OFF   
CONFIG LVP = OFF  

; ========== 变量定义 ==========
            CBLOCK 0x20
input       ; 保存当前要显示的数字
count       ; 计数器
temp1       ; delay用
temp2
            ENDC

; ========== 启动 ==========
ORG 0x0000
    GOTO MAIN

; ========== 中断向量 ==========
ORG 0x0008
    BTFSC INTCON, INT0IF
    CALL INT0_ISR
    RETFIE

; ========== 主程序 ==========
ORG 0x0100
MAIN:
    ; 初始化设置
    MOVLW 0x0F          ; 禁用模拟功能
    MOVWF ADCON1

    CLRF TRISD          ; PORTD 设为输出（接数码管）
    SETF TRISB          ; PORTB 设为输入（INT0 接在 RB0）

    CLRF PORTD          ; 清除初始输出
    CLRF count          ; 初始计数为 0

    ; 设置 INT0
    BCF INTCON, INT0IF
    BSF INTCON, INT0IE
    BCF INTCON2, INTEDG0 ; 下降沿触发
    BSF INTCON, GIE      ; 开启全局中断

; ========== 主循环 ==========
LOOP:
    MOVF count, W
    MOVWF input
    CALL bcd_7seg
    MOVWF PORTD
    GOTO LOOP

; ========== INT0 中断服务 ==========
INT0_ISR:
    INCF count, F
    MOVLW 10
    CPFSGT count        ; 如果 count >= 10
    GOTO skip_reset
    CLRF count          ; 清零
skip_reset:
    CALL delay
    BCF INTCON, INT0IF
    RETURN

; ========== 延迟 ==========
delay:
    MOVLW D'100'
    MOVWF temp1
delay_outer:
    MOVLW D'200'
    MOVWF temp2
delay_inner:
    NOP
    NOP
    DECFSZ temp2, F
    GOTO delay_inner
    DECFSZ temp1, F
    GOTO delay_outer
    RETURN

; ========== 查表转换段码 ==========
input      equ 0x20    
bcd_7seg:
    movlw low bcd_table
    movwf TBLPTRL
    movlw high bcd_table
    movwf TBLPTRH
    movlw upper bcd_table
    movwf TBLPTRU
    movf input, W
    addwf TBLPTRL, F
    movlw 0
    addwfc TBLPTRH
    addwfc TBLPTRU
    tblrd*
    movf TABLAT, W
    return

; ========== 7段码查找表 ==========
bcd_table:
    db 0x3F,0x06,0x5B,0x4F,0x66,0x6D,0x7D,0x07,0x7F,0x6F

    END
```

## 2

**变量定义建议**

```asm
        CBLOCK 0x20
inputL       ; 显示值低字节
inputH       ; 显示值高字节
countL       ; 计数低字节
countH       ; 计数高字节
digit0       ; 个位
digit1       ; 十位
digit2       ; 百位
digit3       ; 千位
temp1
temp2
            ENDC       
```

```asm
(no comment clean version)
CBLOCK 0x20
input
count
TEMP
cycle_num
digit0
digit1
digit2
digit3
temp1
temp2
ENDC
```

**main loop**

```asm
; ========== 主循环 ==========
MAIN_LOOP:
    MOVFF countL, inputL
    MOVFF countH, inputH
    CALL bin_to_bcd       ; inputL:H → digit3~0
    CALL scan_display     ; 多位数码管轮流显示
    GOTO MAIN_LOOP
```

**bin_to_bcd (double dabble algorithm)**: 将 count（假设是 0–9999 的二进制数）转为 4 位 BCD，分别保存在 digit0（个位）到 digit3（千位）中。

```asm
bin_to_bcd:
    ; 输入: count 存储在 memory 中（例如 0x21）
    ; 输出: digit0~digit3 分别存个位到千位的BCD数值

    movf    count, W
    movwf   TEMP         ; 临时变量保存 count
    clrf    digit0
    clrf    digit1
    clrf    digit2
    clrf    digit3

    movlw   .8           ; 要处理8位
    movwf   cycle_num
convert_loop:
    ; 每次循环左移一位，把原始二进制变为BCD
    ; TEMP 的最高位 → digit0最低位 → digit1最低位 → digit2最低位 → digit3最低位
    rlf     digit0, F
    rlf     digit1, F
    rlf     digit2, F
    rlf     digit3, F
    rlf     TEMP, F

    ; 如果某一位大于等于5，加3，BCD调整
    movf    digit0, W
    sublw   .5
    bnc     noadd0
    addlw   .3
    movwf   digit0
noadd0:
    movf    digit1, W
    sublw   .5
    bnc     noadd1
    addlw   .3
    movwf   digit1
noadd1:
    movf    digit2, W
    sublw   .5
    bnc     noadd2
    addlw   .3
    movwf   digit2
noadd2:
    movf    digit3, W
    sublw   .5
    bnc     noadd3
    addlw   .3
    movwf   digit3
noadd3:

    decfsz  cycle_num, F
    goto    convert_loop
    return
```

**scan_display**

```asm
scan_display:
    ; digit0–3 显示到共阳极/共阴极的数码管
    ; 假设PORTD接段码，PORTC低4位控制位选->main 参考 Asg_four page.19

    ; 显示 digit0
    movf    digit0, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x00
    movwf   PORTC
    call    delay_display

    ; 显示 digit1
    movf    digit1, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x01
    movwf   PORTC
    call    delay_display

    ; 显示 digit2
    movf    digit2, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x02
    movwf   PORTC
    call    delay_display

    ; 显示 digit3
    movf    digit3, W
    movwf   input
    call    bcd_7seg
    movwf   PORTD
    movlw   0x03
    movwf   PORTC
    call    delay_display

    return

delay_display:
    movlw   D'50'
    movwf   temp1
wait_loop:
    nop
    nop
    decfsz  temp1, F
    goto    wait_loop
    return
```

**实现4位counter的总程序代码**

```asm
; === 初始设定 ===
    clrf    countL
    clrf    countH

main_loop:
    ; === 每次计数 +1 ===
    incf    countL, F
    btfss   STATUS, Z        ; 如果 countL 变成0（溢出）
    goto    no_carry
    incf    countH, F        ; 高8位 +1
no_carry:

    ; === 二进制转BCD ===
    call    bin_to_bcd

    ; === 显示函数（不断循环轮显）===
    call    scan_display

    goto    main_loop

bin_to_bcd:
    ; 使用 countH:L 合并为16-bit
    movf    countH, W
    movwf   TEMP
    movf    countL, W
    movwf   countL_copy

    clrf    digit0
    clrf    digit1
    clrf    digit2
    clrf    digit3

    movlw   .16         ; 共需要16次循环（16-bit）
    movwf   bit_count

convert_loop:
    ; 左移 digit3~digit0，先传最高位
    rlf     digit0, F
    rlf     digit1, F
    rlf     digit2, F
    rlf     digit3, F

    rlf     countL_copy, F
    rlf     TEMP, F     ; TEMP为高位

    ; BCD 修正（每位>=5 加3）
    movf    digit0, W
    sublw   .5
    bnc     noadd0
    addlw   .3
    movwf   digit0
noadd0:
    movf    digit1, W
    sublw   .5
    bnc     noadd1
    addlw   .3
    movwf   digit1
noadd1:
    movf    digit2, W
    sublw   .5
    bnc     noadd2
    addlw   .3
    movwf   digit2
noadd2:
    movf    digit3, W
    sublw   .5
    bnc     noadd3
    addlw   .3
    movwf   digit3
noadd3:

    decfsz  bit_count, F
    goto    convert_loop
    return

scan_display:
    ; 每次显示一位，例如 digit0
    ; 配合段码表和位选 PORT 输出
    ; 使用延迟做快速轮换看起来像静态显示

    ; 示例: 输出 digit0
    movf    digit0, W
    call    get_7seg_code   ; 返回段码
    movwf   PORTD           ; 段码输出
    movlw   0b0001
    movwf   PORTC           ; 位选第0位
    call    delay

    ; digit1
    movf    digit1, W
    call    get_7seg_code
    movwf   PORTD
    movlw   0b0010
    movwf   PORTC
    call    delay

    ; digit2
    movf    digit2, W
    call    get_7seg_code
    movwf   PORTD
    movlw   0b0100
    movwf   PORTC
    call    delay

    ; digit3
    movf    digit3, W
    call    get_7seg_code
    movwf   PORTD
    movlw   0b1000
    movwf   PORTC
    call    delay

    return

get_7seg_code:
    ; W中是0~9，返回7段码（共阴或共阳自己定义）
    ; 示例为共阴，数字0~9的段码表存在 ROM/table

    addwf   PCL, F
    retlw   0x3F    ; 0
    retlw   0x06    ; 1
    retlw   0x5B    ; 2
    retlw   0x4F    ; 3
    retlw   0x66    ; 4
    retlw   0x6D    ; 5
    retlw   0x7D    ; 6
    retlw   0x07    ; 7
    retlw   0x7F    ; 8
    retlw   0x6F    ; 9
```

# 3

计算阶乘的loop

```asm

```
