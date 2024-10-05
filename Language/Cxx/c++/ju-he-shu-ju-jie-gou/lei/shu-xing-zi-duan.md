# 属性/字段

在 C++ 中，**属性**（**Attributes**）通常指的是类的**数据成员**（也称为**成员变量**），用于存储对象的状态。属性可以是各种类型的数据，包括基本数据类型（如 `int`、`double`、`char` 等）和用户定义的类型（如类、结构体等）。属性是面向对象编程的核心概念之一，通过它们，开发者可以定义对象的状态。

#### 1. 属性的定义

属性通常在类的内部声明，可以具有不同的访问修饰符：

* **公有属性**（`public`）：可以被任何代码访问。
* **保护属性**（`protected`）：只能被类本身和派生类访问。
* **私有属性**（`private`）：只能被类内部的成员函数访问。

#### 2. 属性的示例

以下是一个简单的示例，展示如何在 C++ 中定义和使用属性：

```cpp
#include <iostream>

class Car {
private:
    std::string brand;  // 私有属性
    int year;           // 私有属性

public:
    // 构造函数
    Car(std::string b, int y) : brand(b), year(y) {}

    // 公共方法：获取品牌
    std::string getBrand() const {
        return brand;
    }

    // 公共方法：获取年份
    int getYear() const {
        return year;
    }

    // 公共方法：显示信息
    void displayInfo() const {
        std::cout << "Brand: " << brand << ", Year: " << year << std::endl;
    }
};

int main() {
    Car car("Toyota", 2020); // 创建 Car 对象
    car.displayInfo(); // 输出：Brand: Toyota, Year: 2020

    return 0;
}
```

#### 3. 属性的特性

* **数据封装**：将属性设为私有可以隐藏对象的内部状态，只有通过公共方法才能访问和修改属性，增强了数据安全性。
* **初始化**：属性通常在构造函数中初始化，可以确保对象在创建时处于有效状态。
* **常量访问**：可以使用 `const` 关键字修饰方法，确保方法不会修改类的属性。

#### 4. 属性的注意事项

* **合理选择访问修饰符**：根据属性的使用场景，选择合适的访问修饰符，以确保数据的安全性和完整性。
* **提供访问器和修改器**：通常为私有属性提供公共的访问器（getter）和修改器（setter），以便外部代码能够安全地访问和修改属性。

```cpp
class Person {
private:
    std::string name;
    int age;

public:
    // 获取姓名
    std::string getName() const {
        return name;
    }

    // 设置姓名
    void setName(const std::string& n) {
        name = n;
    }

    // 获取年龄
    int getAge() const {
        return age;
    }

    // 设置年龄
    void setAge(int a) {
        if (a >= 0) { // 确保年龄有效
            age = a;
        }
    }
};
```

#### 5. 总结

在 C++ 中，属性是类的核心组成部分，定义了对象的状态。通过合理使用访问修饰符、构造函数以及访问器和修改器，开发者可以有效地封装数据，确保对象的完整性和安全性。理解和正确使用属性是掌握 C++ 面向对象编程的重要步骤。
