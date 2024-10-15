# td::shared\_ptr、std::weak\_ptr

在C++中，`std::shared_ptr` 和 `std::weak_ptr` 是标准库提供的智能指针，用于更高效、安全地管理资源，特别是动态内存。`std::shared_ptr` 提供了引用计数管理，可以共享同一资源，而 `std::weak_ptr` 是非拥有型指针，用于解决循环引用问题。以下是二者的使用方法及注意事项。

#### 1. `std::shared_ptr` 的基本使用

`std::shared_ptr` 是一种拥有型智能指针，允许多个指针共享同一个动态分配的对象。它使用引用计数来追踪有多少个 `std::shared_ptr` 实例指向同一对象，当引用计数为零时自动释放资源。

**基本示例**

```cpp
#include <iostream>
#include <memory>

class MyClass {
public:
    MyClass() { std::cout << "MyClass constructor\n"; }
    ~MyClass() { std::cout << "MyClass destructor\n"; }
    void display() const { std::cout << "Hello from MyClass\n"; }
};

int main() {
    std::shared_ptr<MyClass> ptr1 = std::make_shared<MyClass>();
    std::shared_ptr<MyClass> ptr2 = ptr1; // 引用计数加1

    std::cout << "Reference count: " << ptr1.use_count() << std::endl; // 输出 2
    ptr1->display();

    return 0; // ptr1 和 ptr2 超出作用域，引用计数为 0，自动释放
}
```

#### 2. `std::weak_ptr` 的基本使用

`std::weak_ptr` 是一种不拥有资源的智能指针，用于解决循环引用问题。它不会增加引用计数，因此不会影响 `std::shared_ptr` 的生命周期。通常用于缓存或观察对象，同时不会干扰对象的生命周期管理。

**使用场景**

假设两个对象 `A` 和 `B` 互相持有对方的 `std::shared_ptr`，会导致循环引用，资源永远不会被释放。可以将其中一个指针替换为 `std::weak_ptr`，从而打破循环引用。

**示例：使用 `std::weak_ptr` 解决循环引用**

```cpp
#include <iostream>
#include <memory>

class B; // 前向声明

class A {
public:
    std::shared_ptr<B> ptrB; // 指向 B 的 shared_ptr
    ~A() { std::cout << "A destroyed\n"; }
};

class B {
public:
    std::weak_ptr<A> ptrA; // 使用 weak_ptr 打破循环引用
    ~B() { std::cout << "B destroyed\n"; }
};

int main() {
    auto a = std::make_shared<A>();
    auto b = std::make_shared<B>();

    a->ptrB = b;
    b->ptrA = a; // 不增加引用计数

    return 0; // A 和 B 正常销毁
}
```

在上面的例子中，`B` 持有一个指向 `A` 的 `std::weak_ptr`，不会增加 `A` 的引用计数。因此，当 `a` 和 `b` 超出作用域时，引用计数都将归零，资源会正确释放。

#### 3. `std::weak_ptr` 的锁定机制

`std::weak_ptr` 不直接访问资源，需要通过 `lock()` 方法将其转换为 `std::shared_ptr`。`lock()` 方法会检查资源是否还有效，如果资源已经被释放，返回一个空的 `std::shared_ptr`。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::shared_ptr<int> sharedPtr = std::make_shared<int>(100);
    std::weak_ptr<int> weakPtr = sharedPtr;

    if (auto lockedPtr = weakPtr.lock()) { // 检查资源是否有效
        std::cout << "Value: " << *lockedPtr << std::endl;
    } else {
        std::cout << "Resource is no longer available.\n";
    }

    sharedPtr.reset(); // 释放资源

    if (auto lockedPtr = weakPtr.lock()) {
        std::cout << "Value: " << *lockedPtr << std::endl;
    } else {
        std::cout << "Resource is no longer available.\n";
    }

    return 0;
}
```

在这个例子中，`weakPtr.lock()` 在 `sharedPtr` 还未被释放时返回有效的 `std::shared_ptr`；当 `sharedPtr` 被释放后，`lock()` 返回空指针。

#### 4. 自定义删除器

`std::shared_ptr` 支持自定义删除器，适用于非内存资源（例如文件句柄、套接字）或需要特殊清理操作的场景。自定义删除器在 `std::shared_ptr` 超出作用域时自动调用。

```cpp
#include <iostream>
#include <memory>

void customDeleter(int* ptr) {
    std::cout << "Custom deleter called\n";
    delete ptr;
}

int main() {
    std::shared_ptr<int> ptr(new int(42), customDeleter);
    return 0; // 自动调用 customDeleter 释放资源
}
```

在此示例中，`customDeleter` 是一个函数，用于释放动态分配的整数。`std::shared_ptr` 在离开作用域时调用此删除器来释放资源。

#### 总结

* `std::shared_ptr` 用于共享同一资源，自动管理生命周期，通过引用计数实现资源自动释放。
* `std::weak_ptr` 是一种非拥有型指针，不影响引用计数，适合解决循环引用问题。
* `lock()` 用于从 `std::weak_ptr` 获取有效的 `std::shared_ptr`，检查资源是否仍然存在。
* 自定义删除器可以在 `std::shared_ptr` 释放资源时执行特殊的清理逻辑。
