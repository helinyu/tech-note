# 虚函数 vs 纯虚函数

在 C++ 中，**虚函数**（**Virtual Function**）和**纯虚函数**（**Pure Virtual Function**）是实现多态性的两个重要概念。它们都是在类中声明的，用于支持运行时多态性，但有一些关键的区别。

#### 1. 虚函数（Virtual Function）

* **定义**：虚函数是在基类中使用 `virtual` 关键字声明的成员函数，它可以在派生类中被重写（**Override**）。
* **功能**：虚函数允许通过基类指针或引用来调用派生类的实现，支持运行时多态性。
* **实例化**：包含虚函数的类可以被实例化。
* **语法**：

```cpp
class Base {
public:
    virtual void show() { // 虚函数
        std::cout << "Base class show function." << std::endl;
    }
};
```

#### 2. 纯虚函数（Pure Virtual Function）

* **定义**：纯虚函数是在基类中声明为虚函数，并在声明时将其初始化为 0，例如：

```cpp
virtual void functionName() = 0;
```

* **功能**：纯虚函数强制要求派生类必须提供具体实现，使得基类成为**抽象类**。抽象类不能被实例化。
* **实例化**：包含纯虚函数的类不能被实例化，只能作为基类使用。
* **语法**：

```cpp
class Base {
public:
    virtual void show() = 0; // 纯虚函数
};
```

#### 3. 主要区别

| 特征   | 虚函数                | 纯虚函数           |
| ---- | ------------------ | -------------- |
| 定义   | 在类中使用 `virtual` 声明 | 在类中使用 `= 0` 声明 |
| 实例化  | 可以被实例化             | 不能被实例化         |
| 需要实现 | 可以选择性地在派生类中重写      | 必须在派生类中实现      |
| 类的类型 | 普通类                | 抽象类            |
| 默认实现 | 可以有默认实现            | 没有实现           |

#### 4. 示例代码

下面是一个简单的示例，演示虚函数和纯虚函数的使用：

```cpp
#include <iostream>

// 基类，包含虚函数
class Base {
public:
    virtual void show() { // 虚函数
        std::cout << "Base class show function." << std::endl;
    }

    virtual ~Base() {} // 虚析构函数
};

// 抽象类，包含纯虚函数
class AbstractBase {
public:
    virtual void show() = 0; // 纯虚函数

    virtual ~AbstractBase() {} // 虚析构函数
};

// 派生类，重写虚函数
class Derived : public Base {
public:
    void show() override { // 重写虚函数
        std::cout << "Derived class show function." << std::endl;
    }
};

// 派生类，实现纯虚函数
class DerivedAbstract : public AbstractBase {
public:
    void show() override { // 实现纯虚函数
        std::cout << "DerivedAbstract class show function." << std::endl;
    }
};

int main() {
    Base* b = new Derived(); // 可以实例化
    b->show(); // 调用派生类的重写方法

    AbstractBase* a = new DerivedAbstract(); // 可以实例化
    a->show(); // 调用派生类的实现方法

    delete b;
    delete a;

    return 0;
}
```

#### 5. 总结

* **虚函数**是允许派生类重写的成员函数，可以被实例化的类。
* **纯虚函数**是必须在派生类中实现的函数，使得基类成为抽象类，不能被实例化。

这两个概念是 C++ 中实现多态性的核心，通过它们，程序员可以编写更灵活和可扩展的代码。

