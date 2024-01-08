---
icon: fontawesome/solid/chalkboard-user
tags: [Updating]
comments: true
---

# Lecture Notes

## 01 Overview

1. **Sign-Magnitude:**

   - **Positive Numbers:** The most significant bit (MSB) is the sign bit (0 for positive).
   - **Negative Numbers:** The sign bit is 1, and the remaining bits represent the magnitude of the negative number.

   Example:

   - `+6` is represented as `0 0110` (sign bit 0, magnitude 6).
   - `-6` is represented as `1 0110` (sign bit 1, magnitude 6).

2. **One's Complement:**

   - **Positive Numbers:** Same as unsigned binary representation.
   - **Negative Numbers:** To represent a negative number, invert (flip) all the bits.

   Example:

   - `+6` is represented as `0 0110`.
   - `-6` is represented as `1 1001` (inverting all bits of `0 0110`).

3. **Two's Complement:**

   - **Positive Numbers:** Same as unsigned binary representation.
   - **Negative Numbers:** To represent a negative number, invert all bits and add 1.

   Example:

   - `+6` is represented as `0 0110`.
   - `-6` is represented as `1 1010` (inverting all bits of `0 0110` and adding 1).

1. Integer overflow:

    ```shell
    (lldb) print 40000 * 40000
    (int) 1600000000
    (lldb) print 50000 * 50000
    (int) -1794967296
    01101010111111010000011100000000 (1794967296)
    bin(int(invert_bits(np.binary_repr(1794967296)[1:]), 2)+1)
    10010101000000101111100100000000 (50000 * 50000)
    ```

    In a 32-bit system:

    $$
    \begin{align*}
      50000 * 50000 &= 2,500,000,000 \\
      2^{31} - 1 &= 2,147,483,647 \\
      2,500,000,000 &> 2,147,483,647 \\
    \end{align*}
    $$

2. Integer arithmetic is commutative and associative.

    ```shell
    (lldb) print 400 * 500 * 600
    (int) 120000000
    (lldb) print 300 * 400 * 500 * 600
    (int) 1640261632
    (lldb) print 400 * 500 * 600 * 300
    (int) 1640261632
    ```

3. Limitations of floating-point arithmetic:

   ```python
   >>> (1e20 + -1e20) + 3.14
   3.14
   >>> 1e20 + (-1e20 + 3.14)
   0.0
   >>> -1e20 + 3.14
   -1e+20
   ```
   
   - `3.14` compared to `-1e+20` is so insignificant.
   
   - [Round-off error in Floats](https://en.wikipedia.org/wiki/Round-off_error)

## 02 Bits, Bytes and Integer

### Bit-level Manipulations

`a = 0110 1001`为`1`的位数`{0,3,5,6}`

`b = 0101 0101`为`1`的位数`{0,2,4,6}`

1. `&` bitwise and 相当于 intersection，ab 的交集为`{0,6} `，`0100 0001`
2. `|` bitwise or 相当于 union，ab 的并集为`{0,2,3,4,5,6}`，`0111 1101`
3. `^` bitwise x-or 相当于 symmetric difference，ab 取不同的值`{2,3,4,5}`，`0011 1100`
4. `~` bitwise not 相当于 complement，b 的补集为`{1,3,5,7}`，`1010 1010`

`c = 1010 0010`

1. Left shift 不区分 Logical 还是 Arithmetic，`c << 3 = 0001 0000`
2. Right shift 区分
    - Logical: Fill with 0’s on left，自左边填充 0，`c Log. >> 2 = 0010 1000`
    - Arithmetic: Replicate most significant bit on left，以符号位的数字填充，`c Arith. >> 2 = 1110 1000`

C Programming:

```c
#include <stdio.h>

int main() {
  unsigned char a = 0b01101001;
  unsigned char b = 0b01010101;
  char c = 0b10100010;
  unsigned char tmp;
  printf("a & b = 0x%x\n", a & b);
  printf("a | b = 0x%x\n", a | b);
  printf("a ^ b = 0x%x\n", a ^ b);
  tmp = ~b;
  printf("~b = 0x%x\n", tmp);
  tmp = c << 3;
  printf("c << 3 = 0x%x\n", tmp);
  tmp = (unsigned char)c >> 2;
  printf("c Log. >> 2 = 0x%x\n", tmp);
  tmp = c >> 2;
  printf("c Arith. >> 2 = 0x%x\n", tmp);
  return 0;
}

/* a & b = 0x41
 * a | b = 0x7d
 * a ^ b = 0x3c
 * ~b = 0xaa
 * c << 3 = 0x10
 * c Log. >> 2 = 0x28
 * c Arith. >> 2 = 0xe8 */
```

1. C 语言，无符号类型移位都是 Logical，其他移位都是 Arithmetic

2. Python 中，右移都是 Arithmetic，负数的`bin, oct, hex`显示的是负的原码，实际存储用的依然是补码，如果想直接打印负数`n`的补码，使用`hex(n & 0xff...f)`，其中`0xff...f`为 word size

    ```python
    >>> bin(3), bin(-3), hex(3), hex(-3), hex(-3 & 0xffffffff)
    ('0b11', '-0b11', '0x3', '-0x3', '0xfffffffd')
    ```

3. Java 中，Logical 右移`>>`，Arithmetic 右移`>>>`

### Numeric Ranges

`w`表示 word size 位数、字长

1. Unsigned Values

    - $UMin=0$ `000...0`

    - $Umax=2^w-1$ `111...1`

2. Two's Complement Values

    - $TMin=-2^w-1$ `100...0`

    - $TMax=2^{w-1}-1$ `011...1`

3. T2B: Two's complement to Bits, U2B: Unsigned to Bits, B2U, B2T, T2U, U2T

4. For $w=16$,

    - $UMax=65535=0xFFFF$

    - $TMax=32767=0x7FFF$

    - $TMin=-32768=0x8000$

    - $-1=0xFFFF$

5. 在 Linux 系统中，数值范围存储在`/usr/include/limits.h`中：

    ```shell
    ❯ cat /usr/include/limits.h | grep 'LONG_MAX\|LONG_MIN'
    #   define LONG_MAX     9223372036854775807L
    #   define LONG_MAX     2147483647L
    #  define LONG_MIN      (-LONG_MAX - 1L)
    #   define ULONG_MAX    18446744073709551615UL
    #   define ULONG_MAX    4294967295UL
    #   define LLONG_MAX    9223372036854775807LL
    #   define LLONG_MIN    (-LLONG_MAX - 1LL)
    #   define ULLONG_MAX   18446744073709551615ULL
    /* The <limits.h> files in some gcc versions don't define LLONG_MIN,
      LLONG_MAX, and ULLONG_MAX.  Instead only the values gcc defined for
    # ifndef LLONG_MIN
    #  define LLONG_MIN     (-LLONG_MAX-1)
    # ifndef LLONG_MAX
    #  define LLONG_MAX     __LONG_LONG_MAX__
    # ifndef ULLONG_MAX
    #  define ULLONG_MAX    (LLONG_MAX * 2ULL + 1)
    ```

### Conversion, casting

C 语言中，unsigned 和 signed 进行比较时，会自动将 signed 转化为 unsigned。在任何地方出现 unsigned 变量，关于它所有的运算都会变成 unsigned。

```c
#include <stdio.h>

int main() {
  int a = -1;
  unsigned int b = 0U;
  printf("%d > %uU = %d\n", a, b, a > b);
  /* a = (1 << 31) - 1; produce overflow warning */
  a = 2147483647;
  b = 1 << 31;
  printf("(int)%uU = %d\n", b, (int)b);
  printf("%d > (int)%uU = %d\n", a, b, a > (int)b);
  return 0;
}

/* -1 > 0U = 1
 * (int)2147483648U = -2147483648
 * 2147483647 > (int)2147483648U = 1 */
```

容易发生的错误，导致死循环：

-   `unsigned i; for (i = n; i >= 0; i--)` `i` always greater than or equal to `0`

-   `int i; for (i = n; i-sizeof(int) >= 0; i--)` `sizeof()` return a unsigned value

### Sign Extension

MSB (Most Significant Bit) 最高有效位，二进制中代表最高值的比特位，这一位对数值的影响最大。LSB (Least Significant Bit) 最低有效位，二进制中代表最低值的比特位。

1. Task:

    - Given `w` bit signed integer `x`

    - Convert it to `w+k` bit integer with same value

2. Rule:

    - Make `k` copies of sign bit:

    - $X'=X_{w-1},\dots,X_{w-1},X_{w-1},X_{w-2},\dots,X_{0}$

    - where $X_{w-1}\dots X_{w-1},X_{w-1}$ are `k` copies of MSB

### Add, multiplication, shifting, negation

1. Add

    - Unsigned: $UAdd_w(u,v)=u+v\ mod\ 2^w$

    - Two's Complement: $u+v\geq2^{w-1}$ positive overflow, sum becomes negative. $u+v\lt-2^{w-1}$ negative overflow, sum becomes positive.

        ```
        negative overflow: char a = -128 - 1 = 127
        positive overflow: unsigned char b = 255 + 1 = 0
        ```

2. Multiplication

    - Unsigned: $UMult_w(u,v)=u\cdot v\ mod\ 2^w$

    - Two's Complement: Ignore high order `w` bits

3. Shift: $u<<k=u\cdot 2^k$, $u>>k=\lfloor{u/2^k}\rfloor$

4. Negation: 对于以 Two's Complement 存储的整数`n`，当$TMin<x\leq TMax$，如果需要 negate 取负值，只需要`~n+1`，即取反加 1

    ```
    int c = 2147483647;
    -c = ~(c) + 1 = -2147483647
    int c = -2147483648;
    -c = -2147483648
    ~(c) + 1 = -2147483648
    ```
