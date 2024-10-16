# 域名空间(namespace)

在 C++ 中，`namespace`（命名空间）用于组织代码并避免命名冲突。通过使用命名空间，你可以将变量、函数、类等定义在一个逻辑区域中，而不会与其他命名空间中的同名符号产生冲突。

#### 主要特性：

1.  **声明命名空间**： 使用 `namespace` 关键字声明命名空间。

    ```cpp
    namespace MyNamespace {
        int value = 42;
        void myFunction() {
            // do something
        }
    }
    ```
2.  **访问命名空间中的成员**： 使用 `::` 作用域解析符访问命名空间中的元素。

    ```cpp
    int main() {
        MyNamespace::myFunction();  // 调用 MyNamespace 中的函数
        int val = MyNamespace::value;  // 访问命名空间中的变量
    }
    ```
3.  **嵌套命名空间**： 命名空间可以嵌套。

    ```cpp
    namespace Outer {
        namespace Inner {
            void innerFunction() {}
        }
    }

    int main() {
        Outer::Inner::innerFunction();  // 访问嵌套的命名空间
    }
    ```
4.  **匿名命名空间**： 匿名命名空间的内容只能在声明它的文件中访问，相当于局部的命名空间。它通常用于避免全局作用域中的符号冲突。

    ```cpp
    namespace {
        int localVar = 100;
    }

    int main() {
        // 可以访问 localVar
        return localVar;
    }
    ```
5.  **`using` 声明**： 使用 `using` 关键字，可以在当前作用域内使用某个命名空间中的所有或特定成员，避免重复使用 `::`。

    ```cpp
    using namespace MyNamespace;

    int main() {
        myFunction();  // 不再需要 MyNamespace:: 前缀
        return value;
    }
    ```

    也可以只导入特定成员：

    ```cpp
    using MyNamespace::myFunction;

    int main() {
        myFunction();  // 只导入 myFunction 而不导入其他成员
    }
    ```
6.  **命名空间别名**： 命名空间可以设置别名，以简化长命名空间的使用。

    ```cpp
    namespace LongNamespaceName = MyNamespace;

    int main() {
        LongNamespaceName::myFunction();  // 使用别名访问命名空间成员
    }
    ```
7.  **标准库命名空间**： C++ 标准库中的所有内容都定义在 `std` 命名空间中。例如，`std::cout`, `std::vector`。

    ```cpp
    #include <iostream>

    int main() {
        std::cout << "Hello, World!" << std::endl;  // 使用 std 命名空间中的 cout
    }
    ```

#### 命名空间的作用

1. **避免命名冲突**：命名空间使得不同开发者或库可以使用相同的名字，而不会引发冲突。
2. **组织代码**：它帮助将代码逻辑分离到不同的区域，提升可读性和维护性。

通过 `namespace`，C++ 提供了一个灵活且高效的方式来管理代码中的命名冲突问题，尤其是在大型项目或使用多个库的情况下。
