---
icon: material/more
tags: [Updating]
comments: true
---

# Misc

1. 配置 [PicGo-Core](https://picgo.github.io/PicGo-Core-Doc/zh/guide/config.html)
2. 注册 [sm.ms](https://smms.app/)

## Binary, Octal, Hexadecimal Literals

`x = 10` in Decimal

1. Binary

    - C `int x = 0b1010`
    - Python `x = '0b1010'` `bin(10)`
    - Java `int x = 0b101`

2. Octal

    - C `int x = 012`
    - Python `x = '0o12'` `oct(10)`
    - Java `int x = 012`

3. Hexadecimal

    - C `int x = 0xa`
    - Python `x = '0xa'` `hex(10)`
    - Java `int x = 0xa`

4. Bitwise operations

    - AND `&`, OR `|`, exclusive OR (XOR) `^`, Complement `~`
    - Left shift `<<`, Right shift `>>`

5. [Operator precedence](https://en.cppreference.com/w/c/language/operator_precedence) 优先级

-   单目运算符 (unary operator) > 双目运算符 (binary operator) > 三目运算符 (ternary operator)

-   `~, !` > 算数运算符 > `<<, >>` > 关系运算符 > 按位运算符 > `&&, ||` > 赋值运算符

## ANSI Escape Code

ANSI: American National Standards Institute

ANSI escape sequences are a standard for in-band signaling to control cursor location, color, font styling, and other options on video text terminals and terminal emulators. The terminal interprets these sequences as commands, rather than text to display verbatim.

一种转义序列标准，用于控制视频文本终端上的光标位置、颜色和其他选项。终端会把这些字节序列解释为相应的指令，而不是一字不差的文本。

最常用的序列代码为[Control Sequence Introducer (CSI)](<https://en.wikipedia.org/wiki/ANSI_escape_code#CSI_(Control_Sequence_Introducer)_sequences>)，`ESC[`，在编码中写为`\033[`。

1. 光标移动：

    ```python
    print('\033[2J\033[1;1f')
    ```

    - `CSI n J`: Erase in Display. If n is 2, clear entire screen (and moves cursor to upper left on DOS ANSI.SYS).

    - `CSI n ; m f`: Horizontal Vertical Position. Moves the cursor to row n, column m.

    - 清屏，移动光标到第 1 行，第 1 列。

2. 指定打印[颜色](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors)：

    ```python
    print("\033[31mRed\033[0m")
    print("\033[32mGreen\033[0m")
    ```

    - `CSI n m`: Select Graphic Rendition (SGR), sets display attributes.
    - `CSI 0 m`: Reset or normal. All attributes off.
    - m in `30-39`: Set foreground color. 红色为 31，绿色为 32。
    - m in `40-49`: Set background color.
    - 以红色输出 Red，以绿色输出 Green。

## Endianness

Endianness is primarily expressed as big-endian (BE) or little-endian (LE). A big-endian system stores the most significant byte of a word at the smallest memory address and the least significant byte at the largest. A little-endian system, in contrast, stores the least-significant byte at the smallest address.

大端模式：高位字节存储在低地址中，低位字节存储在高地址中。小端模式：低位字节存储在低地址中，高位字节存储在高地址中。大部分现代计算机存储模式都为 little-endian，如`x86-64`，还有两种模式都允许的架构，如`ARM, RISC-V`，网络接口传输使用的基本都是 big-endian。

## Regular Expression
