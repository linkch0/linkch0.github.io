---
icon: fontawesome/solid/laptop-code
tags: [Updating]
comments: true
---

# Labs

## 1 Data Lab

1. `isTmax(int x)`，卡在如何区分`0x7ff...f (TMax)`和`0xff...f (-1)`，方法为`!(-1+1)==1`，而`!(n+1)==0, n!=-1`。

2. `int n; n^n == 0`，因此`int a,b; if (a == b)`相当于`if !(a ^ b)`

3. `isAsciiDigit(int x)`，卡在如何判断`0<=n<=9`，方法为`n-10<0`，`-10`为`~10+1`，`<0`则符号为`1`

4. `-1 = 0xFF...F`，`-1`二进制补码为全 1，则`-1^n=~n, -1&n=n, -1|n=-1`，`~0=-1`

5. `int isLessOrEqual(int x, int y)`，思路是符号不同正数为大，二是符号相同看差值符号。符号不同时，相减求差值可能溢出，所以直接判断正数为大；符号相同时相减求差值的符号。

6. `int howManyBits(int x)`，思路：对于`0`，返回`1`；对于正数，返回从补码第一个为`1`以后的 bits 长度`+1`，`+1`为正数的符号位`0`；对于负数，返回补码第一个为`0`以后的 bits 长度`+1`，`+1`为负数的符号位`1`
