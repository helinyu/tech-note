# 函数

C++ 中的函数是程序的基本组成单元，它允许开发者将代码分解成可重用的块。C++ 函数的语法、使用和特性与 C 语言类似，但在 C++ 中，函数有更多高级功能，如函数重载、默认参数、内联函数等。让我们从几个角度来理解 C++ 中的函数。

## 1. **基本函数定义**

C++ 函数由返回类型、函数名、参数列表和函数体组成。以下是一个基本的函数定义：

```cpp
#include <iostream>

int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(3, 5);
    std::cout << "Result: " << result << std::endl;
    return 0;
}
```

* **返回类型**：函数返回的值类型，如 `int`、`void` 等。
* **函数名**：函数的名称，用于调用函数。
* **参数列表**：函数接受的输入参数，可以为空。
* **函数体**：函数执行的代码块。

## 2. **函数声明与定义**

函数声明（也称为函数原型）通常放在程序的顶部或头文件中，提供了函数的签名。函数定义则包含了函数的具体实现。示例：

```cpp
// 函数声明
int add(int, int);

// 函数定义
int add(int a, int b) {
    return a + b;
}

int main() {
    std::cout << add(2, 3) << std::endl;
    return 0;
}
```

函数声明允许编译器提前知道函数的存在，从而可以在定义函数之前使用它。

## 3. **函数参数传递**

在 C++ 中，函数参数可以通过以下三种方式传递：

* **按值传递**（Pass by Value）：函数接收参数的副本，修改函数内部的参数不会影响原始数据。
* **按引用传递**（Pass by Reference）：函数接收参数的引用，修改函数内部的参数会影响原始数据。
* **按指针传递**（Pass by Pointer）：函数接收指针，修改指针所指向的内存地址会影响原始数据。

示例：

```cpp
void byValue(int x) {
    x = 10;  // 只改变了函数内部的副本
}

void byReference(int &x) {
    x = 10;  // 改变了原始变量的值
}

void byPointer(int *x) {
    *x = 10;  // 改变了指针所指向的变量值
}
```

## 4. **默认参数**

C++ 函数支持默认参数，即在函数定义时可以为参数指定默认值。如果调用时不传递该参数，则使用默认值：

```cpp
int multiply(int a, int b = 2) {
    return a * b;
}

int main() {
    std::cout << multiply(5) << std::endl;  // 输出 10
    std::cout << multiply(5, 3) << std::endl;  // 输出 15
    return 0;
}
```

## 5. **函数重载**

C++ 支持函数重载，即可以定义多个具有相同名称但参数不同的函数。编译器会根据调用时传递的参数类型来选择适当的函数版本：

```cpp
int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}

int main() {
    std::cout << add(3, 4) << std::endl;  // 调用 int 版本
    std::cout << add(3.5, 2.1) << std::endl;  // 调用 double 版本
    return 0;
}
```

## 6. **内联函数**

内联函数使用 `inline` 关键字，<mark style="color:orange;">编译器会尝试将函数的调用替换为其函数体，从而避免函数调用的开销。</mark>适用于小函数：

```cpp
inline int square(int x) {
    return x * x;
}

int main() {
    std::cout << square(5) << std::endl;
    return 0;
}
```

内联只是建议，编译器可能会根据情况决定是否实际将函数内联。



## 7. **递归函数**

递归函数是指函数调用自身。递归通常用于分解复杂问题，例如计算阶乘：

```cpp
int factorial(int n) {
    if (n == 0)
        return 1;
    return n * factorial(n - 1);
}

int main() {
    std::cout << "Factorial of 5: " << factorial(5) << std::endl;
    return 0;
}
```

## 8. **函数指针**

函数指针是指向函数的指针，允许动态地选择和调用函数。函数指针的定义与普通指针类似，只是类型为函数签名：

```cpp
int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int main() {
    int (*operation)(int, int);  // 定义函数指针
    operation = add;
    std::cout << operation(3, 4) << std::endl;  // 调用 add

    operation = subtract;
    std::cout << operation(7, 2) << std::endl;  // 调用 subtract
    return 0;
}
```

## 9. **Lambda 表达式**

C++11 引入了 **Lambda 表达式**，**即匿名函数**，允许在代码中定义短小的内联函数。语法类似于函数，但无需显式命名：

```cpp
auto add = [](int a, int b) {
    return a + b;
};

int main() {
    std::cout << add(3, 4) << std::endl;  // 输出 7
    return 0;
}
```

## 10. **模板函数**

模板函数允许编写通用函数，可以处理多种类型的输入。模板函数通过模板参数定义：

```cpp
template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    std::cout << add(3, 4) << std::endl;  // 输出 int 7
    std::cout << add(3.5, 4.2) << std::endl;  // 输出 double 7.7
    return 0;
}
```

#### 总结

C++ 中的函数功能强大且灵活，从基本的函数定义到高级的函数特性（如函数重载、模板函数、Lambda 表达式等），都极大地提高了代码的可重用性和灵活性。理解并熟练掌握这些特性是 C++ 编程的关键。
