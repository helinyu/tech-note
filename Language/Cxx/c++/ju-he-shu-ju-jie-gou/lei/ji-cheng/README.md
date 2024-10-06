# 继承

在 C++ 中，**继承**（**Inheritance**）是面向对象编程的重要特性之一，允许创建一个新类（**派生类**）从一个已有的类（**基类**）扩展。通过继承，派生类可以重用基类的属性和方法，同时可以添加新的特性或重写基类的方法。继承促进了代码的重用和模块化设计。

#### 1. 继承的类型

C++ 支持几种不同类型的继承：

* **公有继承**（Public Inheritance）：派生类可以访问基类的公有成员和保护成员。基类的私有成员在派生类中不可访问。

```cpp
class Base {
public:
    void publicMethod() {}
protected:
    void protectedMethod() {}
private:
    void privateMethod() {}
};

class Derived : public Base {
public:
    void accessMethods() {
        publicMethod();    // 可访问
        protectedMethod(); // 可访问
        // privateMethod(); // 不可访问
    }
};
```

* **保护继承**（Protected Inheritance）：派生类可以访问基类的公有成员和保护成员，但基类的公有成员在派生类外部不可访问。

```cpp
class Derived : protected Base {
public:
    void accessMethods() {
        publicMethod();    // 可访问
        protectedMethod(); // 可访问
        // privateMethod(); // 不可访问
    }
};
```

* **私有继承**（Private Inheritance）：派生类只能在内部访问基类的公有成员和保护成员，基类的公有成员在派生类外部不可访问。

```cpp
class Derived : private Base {
public:
    void accessMethods() {
        publicMethod();    // 可访问
        protectedMethod(); // 可访问
        // privateMethod(); // 不可访问
    }
};
```

#### 2. 继承的示例

以下是一个简单的继承示例，展示了基类和派生类之间的关系：

```cpp
#include <iostream>

// 基类
class Animal {
public:
    void eat() {
        std::cout << "Eating..." << std::endl;
    }
};

// 派生类
class Dog : public Animal {
public:
    void bark() {
        std::cout << "Woof!" << std::endl;
    }
};

int main() {
    Dog dog;
    dog.eat(); // 调用基类方法
    dog.bark(); // 调用派生类方法

    return 0;
}
```

#### 3. 继承的特点

* **代码复用**：派生类可以重用基类的成员（数据和方法），从而减少代码重复。
* **多态性**：通过基类指针或引用，可以实现对派生类对象的操作。这是通过虚函数和动态绑定实现的。
* **层次结构**：继承允许创建层次结构，使得相关类之间的关系更加清晰。

#### 4. 继承的注意事项

* **基类构造函数**：在派生类构造函数中，基类构造函数会自动调用，除非显式指定调用。可以在派生类的构造函数初始化列表中指定基类构造函数。

```cpp
class Base {
public:
    Base() {
        std::cout << "Base constructor called." << std::endl;
    }
};

class Derived : public Base {
public:
    Derived() : Base() { // 调用基类构造函数
        std::cout << "Derived constructor called." << std::endl;
    }
};
```

* **析构函数**：如果基类中有虚函数，基类的析构函数也应该声明为虚函数，以确保在删除派生类对象时能够正确调用析构函数。

```cpp
class Base {
public:
    virtual ~Base() {
        std::cout << "Base destructor called." << std::endl;
    }
};
```

#### 5. 继承的应用场景

* **实现接口**：通过继承，派生类可以实现基类定义的接口，使得类之间具有更好的协作性。
* **实现特化**：通过继承，可以在派生类中添加特定功能，或重写基类的行为。

#### 6. 总结

继承是 C++ 中面向对象编程的重要特性，允许通过创建派生类来扩展已有类。它促进了代码复用和模块化设计，增强了程序的可维护性。理解继承及其使用方式是掌握 C++ 编程的关键。
