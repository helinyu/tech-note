# 虚函数

在 C++ 中，虚函数（**Virtual Function**）是实现运行时多态的重要机制。它们使得基类和派生类之间的函数调用在运行时可以根据对象的实际类型来决定，允许程序在不需要知道具体类型的情况下调用相应的函数实现。下面详细介绍虚函数的概念、特点、使用和示例。

#### 1. 虚函数的定义

虚函数是在基类中使用 `virtual` 关键字声明的成员函数。通过将一个函数声明为虚函数，编译器在编译时会为其创建一个虚函数表（vtable），允许在运行时根据对象的实际类型调用相应的函数实现。

**示例：**

```cpp
#include <iostream>

class Base {
public:
    // 虚函数
    virtual void show() {
        std::cout << "Base class show function called." << std::endl;
    }
};

class Derived : public Base {
public:
    // 重写基类的虚函数
    void show() override {  // 使用 override 明确声明重写
        std::cout << "Derived class show function called." << std::endl;
    }
};

int main() {
    Base* b;               // 基类指针
    Derived d;            // 派生类对象
    b = &d;               // 基类指针指向派生类对象

    b->show();            // 调用派生类的 show() 函数
    return 0;
}
```

#### 2. 虚函数的特点

1. **运行时多态**：
   * 虚函数的主要目的就是支持运行时多态。通过基类指针或引用调用虚函数，系统会在运行时决定调用哪个版本的函数。
2. **需要在基类中声明**：
   * 虚函数必须在基类中使用 `virtual` 关键字进行声明。派生类可以重写虚函数，但不需要在派生类中再次声明为虚函数。
3. **动态绑定**：
   * 当通过基类指针或引用调用虚函数时，编译器不会直接链接到函数，而是使用虚函数表（vtable）进行查找，决定调用哪个具体实现。
4.  **析构函数**：

    * 如果一个类包含虚函数，建议将析构函数也声明为虚函数。这确保了通过基类指针删除派生类对象时，能够正确调用派生类的析构函数，避免资源泄漏。

    ```cpp
    class Base {
    public:
        virtual ~Base() {
            std::cout << "Base destructor called." << std::endl;
        }
    };
    ```
5. **不能在静态函数中使用**：
   * 虚函数不能是静态成员函数，因为静态函数不与任何特定对象关联。
6. **虚函数表**：
   * 每个类会有一个虚函数表（vtable），它是一个包含指向虚函数的指针的数组。每个对象会有一个指针（`vptr`）指向其类的虚函数表。

#### 3. 虚函数的使用

虚函数用于需要基类与派生类之间的多态行为时，例如在实现接口、回调机制和策略模式时非常常见。

**示例：使用虚函数的策略模式**

```cpp
#include <iostream>
#include <vector>

class Shape {
public:
    virtual void draw() = 0;  // 纯虚函数，声明为抽象类
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle." << std::endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a square." << std::endl;
    }
};

int main() {
    std::vector<Shape*> shapes;
    shapes.push_back(new Circle());
    shapes.push_back(new Square());

    for (Shape* shape : shapes) {
        shape->draw();  // 根据对象类型调用相应的 draw() 函数
    }

    // 释放内存
    for (Shape* shape : shapes) {
        delete shape;
    }
    return 0;
}
```

#### 4. 纯虚函数和抽象类

* **纯虚函数**：通过将虚函数声明为 `= 0` 的形式来定义纯虚函数，表示该函数没有实现。这使得包含纯虚函数的类成为抽象类，无法直接实例化。

**示例：**

```cpp
class AbstractClass {
public:
    virtual void pureVirtualFunction() = 0; // 纯虚函数
};

class ConcreteClass : public AbstractClass {
public:
    void pureVirtualFunction() override {
        std::cout << "Implementation of pure virtual function." << std::endl;
    }
};
```

#### 5. 总结

* **虚函数** 是 C++ 中实现运行时多态的关键机制，通过 `virtual` 关键字声明。
* 它们允许基类指针或引用调用派生类中重写的函数，实现动态绑定。
* 使用虚函数可以提高代码的灵活性和可扩展性，尤其在需要不同实现的场景下。
* 在设计类时，应谨慎使用虚函数，确保其设计符合面向对象编程的原则，避免不必要的性能开销。
