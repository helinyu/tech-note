# 模块(Module)

C++ 中的模块主要由以下几个组成部分： C++20支持

#### 1. **模块声明**

模块通过 `module` 关键字进行声明。例如：

```cpp
module my_module;  // 声明模块
```

#### 2. **导出符号**

使用 `export` 关键字将模块中的函数、类等符号导出，以便其他模块或翻译单元可以使用。例如：

```cpp
export int add(int a, int b) {
    return a + b;
}
```

#### 3. **模块接口**

模块的接口部分可以放在单独的文件中，通常使用 `.cppm` 或 `.ixx` 扩展名。接口定义了模块的公共 API。

#### 4. **模块实现**

模块的实现部分可以放在与接口不同的文件中，通常使用 `.cpp` 扩展名。实现部分定义了具体的功能。

#### 5. **导入模块**

在其他文件中使用 `import` 语句导入模块，从而访问其导出的符号。例如：

```cpp
import my_module;  // 导入模块
```

#### 6. **模块包**

编译器将模块的内容编译成一个模块包（例如 `.cppm` 文件），这个包包含所有导出的符号。使用时，编译器只需要编译一次模块包即可。

#### 7. **命名空间**

模块内部可以使用命名空间来进一步组织代码，从而避免命名冲突。例如：

```cpp
namespace math {
    export int multiply(int a, int b) {
        return a * b;
    }
}
```

#### 使用示例

以下是一个简单的 C++ 模块示例：

**my\_math.cppm**（模块接口和实现）：

```cpp
module my_math;  // 声明模块

export int add(int a, int b) {  // 导出函数
    return a + b;
}

export int multiply(int a, int b) {  // 导出函数
    return a * b;
}
```

**main.cpp**（使用模块）：

```cpp
import my_math;  // 导入模块

#include <iostream>

int main() {
    int sum = add(3, 4);  // 使用模块中的函数
    int product = multiply(3, 4);
    
    std::cout << "Sum: " << sum << ", Product: " << product << std::endl;
    return 0;
}
```

#### 总结

模块在 C++ 中提供了一种更高效的组织代码的方式，同时改善了编译效率和代码封装。
