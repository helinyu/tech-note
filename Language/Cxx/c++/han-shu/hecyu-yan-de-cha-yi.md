# 和C语言的差异

C++ 是从 C 语言发展而来的，因此 C++ 中的函数与 C 语言的函数有许多相似之处，但 C++ 引入了一些新功能和增强特性，使得函数在 C++ 中比 C 中更加灵活和强大。以下是 C++ 中的函数与 C 语言中函数的主要差异。

#### 1. **函数重载**

C++ 支持 **函数重载**，即可以定义多个同名函数，只要它们的参数列表不同。函数重载通过参数的类型、数量或顺序来区分。

**示例：**

```cpp
#include <iostream>

int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}

int main() {
    std::cout << add(3, 4) << std::endl;      // 调用 int 版本，输出 7
    std::cout << add(3.5, 4.5) << std::endl;  // 调用 double 版本，输出 8
    return 0;
}
```

在 C 中，同名函数是禁止的，因为 C 不支持函数重载。

#### 2. **默认参数**

C++ 允许函数定义时为参数指定默认值，而 C 语言不支持默认参数。在函数调用时，如果不传递某些参数，则使用这些默认值。

**示例：**

```cpp
#include <iostream>

int add(int a, int b = 5) {
    return a + b;
}

int main() {
    std::cout << add(10) << std::endl;   // 输出 15（使用默认参数）
    std::cout << add(10, 20) << std::endl; // 输出 30
    return 0;
}
```

在 C 中，函数的每个参数都必须明确传递，无法使用默认值。

#### 3. **内联函数**

C++ 引入了 **内联函数**（`inline`），用于减少函数调用的开销。编译器会尝试将内联函数的调用替换为其函数体代码，从而避免实际的函数调用。不过，内联仅是建议，编译器可以决定是否真的内联。

**示例：**

```cpp
#include <iostream>

inline int square(int x) {
    return x * x;
}

int main() {
    std::cout << square(5) << std::endl;  // 输出 25
    return 0;
}
```

C 语言在 C99 之后也支持 `inline`，但它不是 C 的核心特性。

#### 4. **函数模板**

C++ 提供了 **模板函数**，允许编写与类型无关的泛型代码。函数模板使得可以用同一个函数定义处理不同类型的数据。C 语言没有模板机制，只能通过宏（`#define`）来进行简单的泛型编程。

**示例：**

```cpp
#include <iostream>

template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    std::cout << add(3, 4) << std::endl;        // 输出 7
    std::cout << add(3.5, 4.5) << std::endl;    // 输出 8.0
    return 0;
}
```

C 语言只能通过编写不同版本的函数来处理不同类型，或使用宏来模拟模板的部分功能。

#### 5. **引用参数**

C++ 引入了 **引用**（`&`），它允许按引用传递参数。使用引用传递参数类似于通过指针传递参数，但语法更简洁。在 C++ 中，引用更常用于函数参数传递和返回类型，而 C 中没有引用，只能通过指针传递参数。

**示例：**

```cpp
#include <iostream>

void increment(int &x) {  // 按引用传递参数
    x++;
}

int main() {
    int a = 5;
    increment(a);
    std::cout << a << std::endl;  // 输出 6，原始变量被修改
    return 0;
}
```

在 C 语言中，必须使用指针来达到相同的效果：

```c
#include <stdio.h>

void increment(int *x) {  // 通过指针传递参数
    (*x)++;
}

int main() {
    int a = 5;
    increment(&a);
    printf("%d\n", a);  // 输出 6
    return 0;
}
```

#### 6. **Lambda 表达式**

C++11 引入了 **Lambda 表达式**，也称为匿名函数。Lambda 表达式是一种简洁的语法，可以在函数内部定义一个小型的内联函数。这在需要将函数作为参数传递给其他函数时非常有用。C 语言不支持 Lambda 表达式。

**示例：**

```cpp
#include <iostream>

int main() {
    auto add = [](int a, int b) { return a + b; };
    std::cout << add(3, 4) << std::endl;  // 输出 7
    return 0;
}
```

在 C 语言中，没有类似的功能，只能通过定义普通函数或使用宏来实现类似的功能。

#### 7. **类成员函数**

作为面向对象语言，C++ 支持类和类的成员函数。类成员函数可以访问类的私有数据成员，支持封装和对象的行为定义。在 C 中没有类和面向对象的概念，因此也没有类成员函数。

**示例：**

```cpp
#include <iostream>

class MyClass {
public:
    void greet() {
        std::cout << "Hello, World!" << std::endl;
    }
};

int main() {
    MyClass obj;
    obj.greet();  // 输出 Hello, World!
    return 0;
}
```

在 C 中，类似功能只能通过结构体和函数组合来实现，但没有面向对象的封装机制。

#### 8. **命名空间**

C++ 引入了 **命名空间**（`namespace`），用于组织代码并避免名称冲突。在大型项目中，命名空间可以避免多个函数或变量具有相同的名称。C 语言没有命名空间机制，只能通过文件作用域和 `static` 关键字来解决名称冲突问题。

**示例：**

```cpp
#include <iostream>

namespace MathFunctions {
    int add(int a, int b) {
        return a + b;
    }
}

int main() {
    std::cout << MathFunctions::add(3, 4) << std::endl;  // 使用命名空间中的函数，输出 7
    return 0;
}
```

#### 9. **异常处理**

C++ 支持 **异常处理**，通过 `try`、`catch` 和 `throw` 来处理运行时错误。这是一种更结构化的错误处理机制。在 C 中，错误处理通常依赖于返回值和全局变量 `errno`，并没有异常处理的语法。

**示例：**

```cpp
#include <iostream>

int divide(int a, int b) {
    if (b == 0) {
        throw std::runtime_error("Division by zero");
    }
    return a / b;
}

int main() {
    try {
        std::cout << divide(10, 0) << std::endl;
    } catch (const std::exception &e) {
        std::cout << "Error: " << e.what() << std::endl;
    }
    return 0;
}
```

C 语言中只能通过返回错误代码或者设置全局变量来指示错误，例如：

```c
#include <stdio.h>

int divide(int a, int b) {
    if (b == 0) {
        return -1;  // 返回错误码
    }
    return a / b;
}

int main() {
    int result = divide(10, 0);
    if (result == -1) {
        printf("Error: Division by zero\n");
    }
    return 0;
}
```

#### 总结

C++ 中的函数比 C 中的函数更加灵活，提供了诸如函数重载、默认参数、模板函数、引用参数、Lambda 表达式、类成员函数、异常处理等高级功能。这些特性使得 C++ 在编写复杂程序时具有更强的表达力和代码复用能力。而 C 语言的函数更基础，缺乏这些面向对象和泛型编程的能力。
