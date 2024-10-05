# 抽象

C++ 没有直接定义的 **接口** 或 **协议** 的概念。&#x20;

但是是可以通过抽象类 + 虚函数，来定义一个 “接口”的概念；&#x20;

在 C++ 中，**抽象类**（**Abstract Class**）是一种特殊类型的类，它至少包含一个**纯虚函数**（**Pure Virtual Function**）。抽象类用于定义一个接口，可以在多个派生类中实现这个接口的具体细节。抽象类不能被实例化，只能作为基类使用。

#### 1. 抽象类的定义

*   **纯虚函数**：通过在函数声明后使用 `= 0` 的方式定义。例如：

    ```cpp
    virtual void functionName() = 0;
    ```
* 任何包含一个或多个纯虚函数的类都被视为抽象类。

#### 2. 抽象类的特点

* **不能实例化**：抽象类不能被直接实例化。如果尝试实例化抽象类，编译器将报错。
* **可包含其他成员**：抽象类可以包含数据成员、普通成员函数和虚函数，除了纯虚函数以外。
* **派生类实现**：<mark style="color:orange;">派生类必须实现抽象类中的所有纯虚函数，除非派生类本身也被定义为抽象类</mark>。
* **支持多态性**：通过基类指针或引用可以指向任何派生类的对象，实现运行时多态性。

#### 3. 抽象类的示例

以下是一个 C++ 中抽象类的简单示例，定义了一个图形抽象类 `Shape`，并实现了该抽象类的具体类 `Circle` 和 `Rectangle`。

```cpp
#include <iostream>

// 抽象类，定义接口
class Shape {
public:
    // 纯虚函数
    virtual void draw() = 0;  // 绘制形状
    virtual double area() = 0; // 计算面积

    // 虚析构函数
    virtual ~Shape() {}
};

// 派生类，实现抽象类的纯虚函数
class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}

    // 实现纯虚函数
    void draw() override {
        std::cout << "Drawing a circle with radius " << radius << std::endl;
    }

    double area() override {
        return 3.14 * radius * radius; // 计算圆的面积
    }
};

class Rectangle : public Shape {
private:
    double width, height;

public:
    Rectangle(double w, double h) : width(w), height(h) {}

    // 实现纯虚函数
    void draw() override {
        std::cout << "Drawing a rectangle." << std::endl;
    }

    double area() override {
        return width * height; // 计算矩形的面积
    }
};

int main() {
    Shape* shapes[2]; // 创建形状的指针数组
    shapes[0] = new Circle(5.0);   // 创建圆
    shapes[1] = new Rectangle(4.0, 6.0); // 创建矩形

    // 绘制形状并计算面积
    for (int i = 0; i < 2; ++i) {
        shapes[i]->draw(); // 调用各自的绘制方法
        std::cout << "Area: " << shapes[i]->area() << std::endl; // 计算面积
    }

    // 释放内存
    for (int i = 0; i < 2; ++i) {
        delete shapes[i];
    }

    return 0;
}
```

#### 4. 抽象类的使用场景

抽象类通常用于以下情况：

* **定义接口**：当希望定义一个接口供多个类实现时，可以使用抽象类。
* **实现多态性**：抽象类允许使用基类指针或引用来操作派生类对象，从而实现运行时多态性。
* **代码复用**：抽象类可以包含实现的公共部分，减少代码重复，提高代码的可维护性。

#### 5. 设计抽象类的注意事项

* **职责单一**：设计抽象类时，要确保接口清晰且职责单一。
* **提供良好的文档**：在定义抽象类和其纯虚函数时，提供良好的文档说明，以便实现类理解其功能和要求。
* **虚析构函数**：为了确保通过基类指针删除派生类对象时能够正确调用析构函数，抽象类应具有虚析构函数。

#### 6. 总结

抽象类在 C++ 中是通过包含纯虚函数的类实现的，提供了一种定义接口的方式，使得不同的类可以实现这些接口。抽象类支持多态性，允许开发者在不关心具体实现的情况下，使用基类指针或引用进行操作。这种设计使得代码更加模块化、灵活和可维护，是面向对象编程中的重要特性之一。

