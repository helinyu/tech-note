# 删除器

**删除器（Deleter）** 是C++中用来释放 `std::unique_ptr` 所管理对象的资源的机制。它为智能指针在其生命周期结束时提供了一种自动释放资源的方式。默认情况下，`std::unique_ptr` 使用 `delete` 操作符作为删除器，用于释放单个动态分配的对象，但在一些特定情况下，我们可以指定自定义的删除器以满足特殊的资源管理需求。

#### 删除器的作用

* **内存释放**：`std::unique_ptr` 会在它超出作用域或被重新分配时调用删除器释放内存。
* **资源管理**：自定义删除器可以管理非内存资源（如文件、套接字、数据库连接）或数组等需要特殊释放的资源。
* **灵活性**：允许开发者根据需要自定义释放逻辑，而不仅限于默认的 `delete` 操作。

#### 删除器的类型

1. **默认删除器**：`std::unique_ptr` 默认使用 `delete` 或 `delete[]` 来释放单个对象或数组内存。
2. **自定义删除器**：可以通过 Lambda 表达式、函数或仿函数来定义，满足特定资源管理的需求。

#### 使用示例

**1. 默认删除器**

对于 `std::unique_ptr`，默认删除器就是 `delete` 或 `delete[]`：

```cpp
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> ptr(new int(5)); // 使用默认删除器 delete
    std::cout << "Value: " << *ptr << std::endl;
    return 0; // ptr 超出作用域时，调用 delete 释放内存
}
```

**2. 使用 Lambda 表达式作为自定义删除器**

Lambda 表达式可以作为删除器用于非内存资源管理，例如关闭文件：

```cpp
#include <iostream>
#include <memory>
#include <cstdio>

int main() {
    auto deleter = [](FILE* file) {
        if (file) {
            std::cout << "Closing file\n";
            fclose(file);
        }
    };

    std::unique_ptr<FILE, decltype(deleter)> filePtr(fopen("example.txt", "w"), deleter);

    if (filePtr) {
        std::cout << "File opened\n";
    }

    return 0; // filePtr 超出作用域时自动调用 fclose 关闭文件
}
```

**3. 使用函数作为自定义删除器**

定义一个独立的函数来作为删除器，适用于需要 `delete[]` 释放动态数组等情况：

```cpp
#include <iostream>
#include <memory>

void arrayDeleter(int* ptr) {
    std::cout << "Deleting integer array\n";
    delete[] ptr;
}

int main() {
    std::unique_ptr<int[], decltype(&arrayDeleter)> arrayPtr(new int[10], arrayDeleter);

    return 0; // arrayDeleter 会自动调用 delete[] 释放数组内存
}
```

**4. 使用仿函数（函数对象）作为自定义删除器**

可以定义一个仿函数（函数对象）类来作为删除器，适合于需要多次调用的删除逻辑：

```cpp
#include <iostream>
#include <memory>

struct CustomDeleter {
    void operator()(int* ptr) const {
        std::cout << "Deleting integer with CustomDeleter\n";
        delete ptr;
    }
};

int main() {
    std::unique_ptr<int, CustomDeleter> ptr(new int(42));
    return 0; // 使用 CustomDeleter 删除指针
}
```

#### 结论

删除器是智能指针的一项重要特性，使得资源管理更加灵活、方便。在 C++ 中，自定义删除器允许我们在 `std::unique_ptr` 的生命周期结束时执行特定的清理操作，从而实现自动化和安全的资源管理。





C和OC中的onExit， 就是该语言定义的一个删除器。

