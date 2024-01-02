---
icon: material/language-c
tags: [Updating]
comments: true
---

# Clang

## X Macro

1. X 宏：

    ```c
    #include <stdio.h>
    #include <unistd.h>

    #define REGS_FOREACH(_)  _(X) _(Y)
    #define RUN_LOGIC        X1 = !X && Y; \
                            Y1 = !X && !Y;
    #define DEFINE(X)        static int X, X##1;
    #define UPDATE(X)        X = X##1;
    #define PRINT(X)         printf(#X " = %d; ", X);

    int main() {
     REGS_FOREACH(DEFINE);
     while (1) { // clock
       RUN_LOGIC;
       REGS_FOREACH(PRINT);
       REGS_FOREACH(UPDATE);
       putchar('\n'); sleep(1);
     }
    }
    ```

2. `gcc -E x_macro.c`，最后几行结果：

    ```c
    int main() {
     static int X, X1; static int Y, Y1;;
     while (1) {
       X1 = !X && Y; Y1 = !X && !Y;;
       printf("X" " = %d; ", X); printf("Y" " = %d; ", Y);;
       X = X1; Y = Y1;;
       putchar('\n'); sleep(1);
     }
    }
    ```

    `printf("1" " 2" " 3\n");` 在编译的时候会把多个双引号的内容合并，相当于`printf("1 2 3\n");`

3. `man gcc`，查看`-E`：

    ```
          -E  Stop after the preprocessing stage; do not run the
              compiler proper.  The output is in the form of
              preprocessed source code, which is sent to the standard
              output.

              Input files that don't require preprocessing are ignored.
    ```

##
