# 函数

C 语言中的函数是编程的基本单元，它允许开发者将代码逻辑分成模块化、可重用的部分。函数可以执行特定的任务，并且可以通过参数传递数据。C 语言的函数与其他现代编程语言的函数概念类似，但 C 语言的函数相对比较基础，支持的功能相对较少。以下是关于 C 语言函数的详细介绍。

#### 1. **函数的定义与调用**

C 语言函数由 **返回类型**、**函数名**、**参数列表** 和 **函数体** 组成。以下是一个典型的 C 语言函数定义：

```c
#include <stdio.h>

// 函数声明（也称为原型）
int add(int a, int b);

int main() {
    int result = add(3, 5);  // 调用函数
    printf("Result: %d\n", result);
    return 0;
}

// 函数定义
int add(int a, int b) {
    return a + b;
}
```

* **返回类型**：指定函数返回值的类型。例如 `int` 表示返回整数类型，`void` 表示无返回值。
* **函数名**：函数的名称，用于在程序中调用该函数。
* **参数列表**：括号中的参数表示函数可以接收的输入，参数类型和参数名称需要声明。
* **函数体**：用 `{}` 包围的代码块，表示函数的具体实现。

#### 2. **函数声明与定义**

* **函数声明**（也称为函数原型）：告知编译器函数的名称、参数和返回类型，通常放在源文件的顶部或头文件中，便于函数定义之后可以调用。
* **函数定义**：是函数的具体实现，包含函数的逻辑代码。

示例：

```c
// 函数声明
int add(int, int);

// 函数定义
int add(int a, int b) {
    return a + b;
}
```

#### 3. **函数参数传递**

C 语言函数支持按值传递和通过指针传递参数：

**按值传递**

按值传递意味着函数接收的是参数的副本，函数内部对参数的修改不会影响原始变量。

```c
void increment(int x) {
    x = x + 1;  // 仅修改副本
}

int main() {
    int a = 5;
    increment(a);
    printf("%d\n", a);  // 输出 5，原始变量未被修改
    return 0;
}
```

**按指针传递**

通过传递指针，函数可以修改原始变量的值，因为指针指向的是原变量的内存地址。

```c
void increment(int *x) {
    *x = *x + 1;  // 修改原始变量
}

int main() {
    int a = 5;
    increment(&a);
    printf("%d\n", a);  // 输出 6，原始变量被修改
    return 0;
}
```

#### 4. **返回值**

函数可以有返回值，返回值类型在函数定义时声明。如果函数不返回值，使用 `void` 作为返回类型。

**有返回值的函数：**

```c
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(4, 5);
    printf("%d\n", result);  // 输出 9
    return 0;
}
```

**无返回值的函数：**

```c
void printMessage() {
    printf("Hello, World!\n");
}

int main() {
    printMessage();  // 调用无返回值的函数
    return 0;
}
```

#### 5. **递归函数**

C 语言支持递归函数，即函数调用自身。这种方法通常用于解决分治问题，例如计算阶乘：

```c
int factorial(int n) {
    if (n == 0)
        return 1;
    return n * factorial(n - 1);  // 递归调用自身
}

int main() {
    printf("Factorial of 5: %d\n", factorial(5));  // 输出 120
    return 0;
}
```

#### 6. **函数指针**

函数指针是指向函数的指针，允许将函数作为参数传递给其他函数。函数指针可以用于实现回调函数等功能。

**定义函数指针并调用函数：**

```c
int add(int a, int b) {
    return a + b;
}

int main() {
    // 定义函数指针
    int (*funcPtr)(int, int);
    
    // 将 add 函数的地址赋值给函数指针
    funcPtr = add;
    
    // 通过函数指针调用函数
    int result = funcPtr(2, 3);
    printf("%d\n", result);  // 输出 5
    return 0;
}
```

**将函数作为参数传递：**

```c
int add(int a, int b) {
    return a + b;
}

int calculate(int (*operation)(int, int), int a, int b) {
    return operation(a, b);  // 调用传递的函数
}

int main() {
    int result = calculate(add, 5, 3);  // 将 add 函数作为参数传递
    printf("%d\n", result);  // 输出 8
    return 0;
}
```

#### 7. **内联函数（C99 之后）**

C 语言从 C99 开始引入了 `inline` 关键字，允许内联函数。内联函数是提示编译器将函数调用替换为其代码体，减少函数调用的开销。

```c
inline int square(int x) {
    return x * x;
}

int main() {
    printf("%d\n", square(5));  // 输出 25
    return 0;
}
```

#### 8. **库函数**

C 语言标准库中提供了大量的库函数，它们分布在不同的头文件中，可以通过 `#include` 指令来引入。例如：

* `printf` 和 `scanf` 在 `<stdio.h>` 头文件中。
* `malloc` 和 `free` 在 `<stdlib.h>` 头文件中。
* `strlen` 和 `strcpy` 在 `<string.h>` 头文件中。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "Hello, World!";
    printf("Length of string: %lu\n", strlen(str));  // 使用 strlen 库函数
    return 0;
}
```

#### 9. **变量的作用域和生命周期**

C 语言中的变量作用域和生命周期与函数密切相关：

* **局部变量**：在函数内部定义，只在该函数内有效，函数执行完毕后其生命周期结束。
* **全局变量**：在函数外部定义，整个程序范围内都有效，直到程序结束时生命周期结束。
* **静态变量**：使用 `static` 关键字声明的变量具有静态存储期，即使在函数调用结束后也保持其值不变，且只在函数范围内可见。

```c
void func() {
    static int count = 0;  // 静态变量
    count++;
    printf("Count: %d\n", count);
}

int main() {
    func();  // 输出 1
    func();  // 输出 2
    return 0;
}
```

#### 10. **头文件与多文件编程**

在大型项目中，函数通常分散在多个源文件中。通过头文件，可以将函数声明与实现分离，允许多个源文件之间共享函数定义。

```c
// add.h - 头文件
#ifndef ADD_H
#define ADD_H

int add(int a, int b);

#endif
```

```c
// add.c - 函数实现
#include "add.h"

int add(int a, int b) {
    return a + b;
}
```

```c
// main.c - 主程序
#include <stdio.h>
#include "add.h"

int main() {
    int result = add(4, 6);
    printf("%d\n", result);  // 输出 10
    return 0;
}
```

#### 总结

C 语言中的函数是代码组织和复用的重要工具，提供了基本的模块化功能。通过理解函数的定义、调用、参数传递、递归、函数指针等特性，可以编写结构良好、易于维护的 C 程序。
