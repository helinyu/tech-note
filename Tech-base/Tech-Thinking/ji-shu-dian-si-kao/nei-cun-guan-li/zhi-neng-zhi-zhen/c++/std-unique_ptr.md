# std::unique\_ptr

在C++中，`std::unique_ptr` 是一种独占型的智能指针，它拥有所指向的对象的唯一所有权，确保同一对象不会被多个指针共享。它通过自动释放内存来防止内存泄漏，非常适用于局部对象的内存管理。

#### 1. 创建和使用 `std::unique_ptr`

要使用 `std::unique_ptr`，首先包含头文件 `<memory>`：

```cpp
#include <memory>
#include <iostream>

class MyClass {
public:
    MyClass() { std::cout << "MyClass constructor\n"; }
    ~MyClass() { std::cout << "MyClass destructor\n"; }
    void display() const { std::cout << "Hello from MyClass\n"; }
};

int main() {
    // 使用 std::make_unique 创建 unique_ptr
    std::unique_ptr<MyClass> ptr = std::make_unique<MyClass>();

    // 访问对象成员
    ptr->display();

    return 0; // ptr 在这里自动释放内存
}
```

在这个示例中，`std::make_unique<MyClass>()` 分配了 `MyClass` 的新实例，并将其所有权交给 `ptr`。当 `ptr` 超出作用域时，`MyClass` 的析构函数会被调用，自动释放内存。

#### 2. 转移所有权

`std::unique_ptr` 不支持复制（拷贝构造和赋值操作被禁用），但可以通过 `std::move` 将所有权转移给另一个 `std::unique_ptr`。

```cpp
int main() {
    std::unique_ptr<MyClass> ptr1 = std::make_unique<MyClass>();
    
    // 将所有权从 ptr1 转移到 ptr2
    std::unique_ptr<MyClass> ptr2 = std::move(ptr1);

    if (!ptr1) {
        std::cout << "ptr1 is now empty\n";
    }
    
    ptr2->display(); // ptr2 现在拥有对象的所有权

    return 0;
}
```

在这个示例中，`std::move(ptr1)` 将 `ptr1` 的所有权转移给 `ptr2`，此时 `ptr1` 变为空，不能再访问该对象。

#### 3. 释放对象

如果希望手动释放对象，可以调用 `unique_ptr` 的 `reset()` 函数：

```cpp
int main() {
    std::unique_ptr<MyClass> ptr = std::make_unique<MyClass>();

    ptr->display();

    // 释放对象，ptr 不再指向任何对象
    ptr.reset();

    if (!ptr) {
        std::cout << "ptr is now empty after reset\n";
    }

    return 0;
}
```

在这里，`ptr.reset()` 释放了 `MyClass` 的内存，将 `ptr` 设置为空。调用 `reset()` 的另一个用途是重新分配新的对象：

```cpp
ptr.reset(new MyClass()); // 分配新的 MyClass 对象
```

#### 4. 自定义删除器

在一些需要特殊释放资源的场景，可以为 `std::unique_ptr` 提供自定义删除器：

```cpp
int main() {
    auto deleter = [](MyClass* p) {
        std::cout << "Custom deleter called\n";
        delete p;
    };

    std::unique_ptr<MyClass, decltype(deleter)> ptr(new MyClass, deleter);
    
    ptr->display();

    return 0; // 使用自定义删除器释放内存
}
```

在这里，`ptr` 会在超出作用域时调用自定义[删除器 `deleter`](https://app.gitbook.com/s/Xko7hXP8ZNDwNDAKRAZr/c/qi-ta/onexit-gai-nian)，以自定义的方式释放资源。

可以参考[C的onExit](https://app.gitbook.com/s/Xko7hXP8ZNDwNDAKRAZr/c/qi-ta/onexit-gai-nian)以及[OC的删除器onExit](https://app.gitbook.com/s/Xko7hXP8ZNDwNDAKRAZr/objective-c/qi-ta/onexit-gai-nian)
