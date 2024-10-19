# 现代语言与智能指针

智能指针是一种在现代编程语言中广泛使用的概念，特别是在面向对象的语言中。智能指针用于自动管理动态分配的内存，帮助开发者减少内存泄漏和悬挂指针的风险。

1. **C++**：C++标准库提供了<mark style="color:red;">多种智能指针</mark>，例如 `std::unique_ptr`、`std::shared_ptr` 和 `std::weak_ptr`，用于实现不同的内存管理策略。
2. **Rust**：Rust 的所有权系统<mark style="color:orange;">内置了智能指针</mark>的概念，如 `Box`、`Rc` 和 `Arc`，通过所有权和借用机制来管理内存。
3. **Swift**：Swift 使用引用计数（ARC）来管理对象的内存，虽然不是传统意义上的智能指针，但提供了类似的功能。
4. **Objective-C**：Objective-C 也支持 ARC，用于自动管理对象的内存，减少手动管理的复杂性。
5. **Java**：Java 使用垃圾回收机制来管理内存，不直接提供智能指针，但概念上类似于智能指针的内存管理。
6. **C#**：C# 也使用垃圾回收来管理内存，提供了一些类似智能指针的功能，例如 `WeakReference`。

虽然并非所有现代语言都有名为“智能指针”的特性，但许多语言都实现了类似的内存管理机制，以提高安全性和降低内存管理的复杂性。