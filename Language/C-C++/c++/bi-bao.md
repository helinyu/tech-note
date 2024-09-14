# 闭包

在 C++中，**闭包（Closure）是可以捕获外部变量的函数对象**。**通常通过 lambda 表达式来实现闭包的功能。**

## **一、lambda 表达式简介**

lambda 表达式的基本语法是：

```cpp
[capture list](parameters)->return type{body}
```

* `capture list`（捕获列表）：用于指定 lambda 表达式可以访问的外部变量。可以按值捕获（`[=]`）、按引用捕获（`[&]`）或混合捕获。
* `parameters`（参数列表）：与普通函数的参数列表类似。
* `return type`（返回类型）：如果可以由编译器推断出返回类型，可以省略。
* `body`（函数体）：包含 lambda 表达式的具体实现。

## **二、闭包的示例**

以下是一个使用 lambda 表达式实现闭包的例子：

```cpp
#include <iostream>

int main() {
    int x = 10;
    auto closure = [x](int y) {
        return x + y;
    };

    std::cout << closure(5) << std::endl; // 输出 15

    return 0;
}
```

在这个例子中，lambda 表达式捕获了外部变量`x`的值，形成了一个闭包。当调用`closure(5)`时，闭包中的函数体使用捕获的`x`的值和传入的参数`y`进行计算并返回结果。

## **三、按引用捕获和可变 lambda**

### 1. 按引用捕获：

如果希望 lambda 表达式修改外部变量的值，可以按引用捕获：

```cpp
#include <iostream>

int main() {
    int x = 10;
    auto closure = [&x](int y) {
        x += y;
        return x;
    };

    std::cout << closure(5) << std::endl; // 输出 15
    std::cout << x << std::endl; // 输出 15，因为 x 被修改了

    return 0;
}
```

### 2. 可变 lambda：

即使按值捕获外部变量，如果希望在 lambda 表达式中修改这些变量，可以使用`mutable`关键字：

```cpp
#include <iostream>

int main() {
    int x = 10;
    auto closure = [x]() mutable {
        x++;
        return x;
    };

    std::cout << closure() << std::endl; // 输出 11
    std::cout << x << std::endl; // 输出 10，因为按值捕获的变量在 lambda 表达式中的修改不会影响外部变量

    return 0;
}
```

## **四、闭包的用途**

1. 作为函数参数：
   * 可以将 lambda 表达式作为参数传递给其他函数，实现更加灵活的编程。
   * 例如，在排序算法中，可以使用 lambda 表达式指定排序的规则。
2. 局部函数对象：
   * 在局部作用域中创建函数对象，避免定义全局函数或成员函数。
   * 可以提高代码的封装性和可读性。
3. 异步编程：
   * 在异步操作中，闭包可以捕获上下文信息，以便在异步操作完成后进行正确的处理。

总之，C++中的 lambda 表达式提供了一种方便的方式来创建闭包，使得代码更加简洁、灵活和易于维护。
