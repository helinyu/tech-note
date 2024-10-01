# 模板泛化vs特化

在C++中，**模板泛化**和**模板特化**是模板编程中的两个重要概念，用于处理不同类型的数据或对象。让我们分别详细解释这两个概念：

#### 1. 模板泛化（Template Generalization）

**模板泛化**指的是模板的默认版本，它为一组类型（通常是任意类型）提供通用的实现。

* **概念**：模板泛化定义了一种通用的行为或逻辑，适用于所有类型。在没有特定要求时，编译器将使用模板的泛化版本。
*   **例子**：

    ```cpp
    template<typename T>
    struct MyTemplate {
        void print() {
            std::cout << "This is a generalized template." << std::endl;
        }
    };
    ```

    这里的`MyTemplate<T>`是一个泛化的模板，它可以适用于任何类型`T`。例如，可以用`int`、`double`、`char`等类型实例化它：

    ```cpp
    MyTemplate<int> obj1;
    MyTemplate<double> obj2;
    ```

    不论`T`是什么类型，上面的泛化模板会执行相同的逻辑。

#### 2. 模板特化（Template Specialization）

**模板特化**指的是针对某些特定类型的模板实现。在模板泛化不能满足需求的情况下，我们可以为某些类型提供专门的实现。这使得我们可以在处理特殊类型时覆盖通用模板的行为。

**两种模板特化：**

* **完全特化（Full Specialization）**：对模板参数完全特定化，针对某个特定类型或一组类型提供实现。
* **部分特化（Partial Specialization）**：针对模板参数的一部分特定化，允许保留部分通用行为，而对某些类型进行特殊处理。

**完全特化的例子：**

```cpp
template<>
struct MyTemplate<int> {
    void print() {
        std::cout << "This is a fully specialized template for int." << std::endl;
    }
};
```

* 在这个例子中，`MyTemplate<int>`是`MyTemplate`模板的完全特化版本，只适用于`int`类型。对于`int`类型，它会输出不同的信息。

**部分特化的例子：**

```cpp
template<typename T>
struct MyTemplate<T*> { // 部分特化指针类型
    void print() {
        std::cout << "This is a partially specialized template for pointers." << std::endl;
    }
};
```

* 在这里，我们对指针类型`T*`进行部分特化。如果我们使用指针类型作为模板参数，它会使用这个特化版本。

例如：

```cpp
MyTemplate<int*> obj3;  // 使用部分特化版本
MyTemplate<double*> obj4;  // 使用部分特化版本
```

#### 区别与用途

* **模板泛化**：提供一套通用逻辑，适用于所有类型，广泛使用于常见情况。
* **模板特化**：用于特定类型提供特殊逻辑，处理泛化模板无法很好处理的情况。

**总结**：模板泛化定义了通用模板逻辑，而模板特化允许在特定类型或情况下覆盖该通用逻辑。
