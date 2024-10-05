# 成员函数(方法)

在 C++ 中，成员函数（Member Functions）是定义在类中的函数，它们与特定对象实例相关联。成员函数可以访问类的成员变量（数据成员），并且可以在类的实例上调用。以下是关于 C++ 中成员函数的基本概念、类型、特点和示例。

#### 1. 成员函数的定义

成员函数是在类定义内部或外部声明的函数。它们可以在类的外部实现，但需要在类内声明。

**示例：**

```cpp
#include <iostream>

class MyClass {
public:
    // 成员变量
    int value;

    // 成员函数的声明
    void setValue(int v);  // 声明成员函数
    void display();         // 声明成员函数
};

// 成员函数的实现
void MyClass::setValue(int v) {
    value = v;  // 访问成员变量
}

void MyClass::display() {
    std::cout << "Value: " << value << std::endl;  // 输出成员变量
}

int main() {
    MyClass obj;  // 创建 MyClass 的对象
    obj.setValue(10);  // 调用成员函数
    obj.display();      // 输出：Value: 10
    return 0;
}
```

#### 2. 成员函数的类型

成员函数可以根据其功能和行为的不同分为几种类型：

**2.1 普通成员函数**

* 普通成员函数可以访问和修改类的成员变量。
* 它们的第一个参数隐式地是对象本身（`this` 指针）。

**2.2 常量成员函数**

* 常量成员函数通过 `const` 关键字进行修饰，表示该函数不会修改类的成员变量。
* 常量成员函数可以被 const 对象调用。

**示例：**

```cpp
class MyClass {
public:
    int value;

    MyClass(int v) : value(v) {}

    void display() const {  // 常量成员函数
        std::cout << "Value: " << value << std::endl;
    }
};
```

**2.3 静态成员函数**

* 静态成员函数属于类本身，而不是任何特定对象。
* 静态成员函数不能访问非静态成员变量和非静态成员函数，因为它们不与任何特定对象关联。

**示例：**

```cpp
class MyClass {
public:
    static int count;  // 静态成员变量

    MyClass() {
        count++;  // 每创建一个对象，count 增加
    }

    static void showCount() {  // 静态成员函数
        std::cout << "Count: " << count << std::endl;
    }
};

int MyClass::count = 0;  // 静态成员变量初始化

int main() {
    MyClass obj1;
    MyClass obj2;
    MyClass::showCount();  // 输出：Count: 2
    return 0;
}
```

#### 3. 成员函数的访问权限

C++ 支持三种访问修饰符，控制成员函数的访问权限：

* **public**：公有成员，可以在类的外部访问。
* **protected**：受保护成员，仅在该类及其派生类中可访问。
* **private**：私有成员，仅在该类内可访问。

#### 4. 成员函数的重载

成员函数可以重载，这意味着可以定义多个同名的成员函数，只要它们的参数类型或数量不同。

**示例：**

```cpp
class MyClass {
public:
    void display(int value) {
        std::cout << "Integer: " << value << std::endl;
    }

    void display(double value) {
        std::cout << "Double: " << value << std::endl;
    }
};

int main() {
    MyClass obj;
    obj.display(5);      // 输出：Integer: 5
    obj.display(3.14);   // 输出：Double: 3.14
    return 0;
}
```

#### 5. 成员函数的调用

可以通过对象调用成员函数，也可以通过类的引用或指针调用。

**示例：**

```cpp
class MyClass {
public:
    void greet() {
        std::cout << "Hello, World!" << std::endl;
    }
};

int main() {
    MyClass obj;
    obj.greet();  // 通过对象调用

    MyClass* ptr = &obj;
    ptr->greet();  // 通过指针调用

    MyClass& ref = obj;
    ref.greet();  // 通过引用调用
    return 0;
}
```

#### 6. 总结

* 成员函数是 C++ 类的重要组成部分，定义了类的行为。
* 可以根据功能分为普通成员函数、常量成员函数和静态成员函数。
* 成员函数的访问权限受访问修饰符的影响。
* 成员函数可以重载，并且可以通过对象、指针和引用进行调用。

成员函数提供了在类内部操作数据成员和实现功能的能力，是 C++ 面向对象编程的核心特性之一。在 C++ 中，成员函数（Member Functions）是定义在类中的函数，它们与特定对象实例相关联。成员函数可以访问类的成员变量（数据成员），并且可以在类的实例上调用。以下是关于 C++ 中成员函数的基本概念、类型、特点和示例。

#### 1. 成员函数的定义

成员函数是在类定义内部或外部声明的函数。它们可以在类的外部实现，但需要在类内声明。

**示例：**

```cpp
#include <iostream>

class MyClass {
public:
    // 成员变量
    int value;

    // 成员函数的声明
    void setValue(int v);  // 声明成员函数
    void display();         // 声明成员函数
};

// 成员函数的实现
void MyClass::setValue(int v) {
    value = v;  // 访问成员变量
}

void MyClass::display() {
    std::cout << "Value: " << value << std::endl;  // 输出成员变量
}

int main() {
    MyClass obj;  // 创建 MyClass 的对象
    obj.setValue(10);  // 调用成员函数
    obj.display();      // 输出：Value: 10
    return 0;
}
```

#### 2. 成员函数的类型

成员函数可以根据其功能和行为的不同分为几种类型：

**2.1 普通成员函数**

* 普通成员函数可以访问和修改类的成员变量。
* 它们的第一个参数隐式地是对象本身（`this` 指针）。

**2.2 常量成员函数**

* 常量成员函数通过 `const` 关键字进行修饰，表示该函数不会修改类的成员变量。
* 常量成员函数可以被 const 对象调用。

**示例：**

```cpp
class MyClass {
public:
    int value;

    MyClass(int v) : value(v) {}

    void display() const {  // 常量成员函数
        std::cout << "Value: " << value << std::endl;
    }
};
```

**2.3 静态成员函数**

* 静态成员函数属于类本身，而不是任何特定对象。
* 静态成员函数不能访问非静态成员变量和非静态成员函数，因为它们不与任何特定对象关联。

**示例：**

```cpp
class MyClass {
public:
    static int count;  // 静态成员变量

    MyClass() {
        count++;  // 每创建一个对象，count 增加
    }

    static void showCount() {  // 静态成员函数
        std::cout << "Count: " << count << std::endl;
    }
};

int MyClass::count = 0;  // 静态成员变量初始化

int main() {
    MyClass obj1;
    MyClass obj2;
    MyClass::showCount();  // 输出：Count: 2
    return 0;
}
```

#### 3. 成员函数的访问权限

C++ 支持三种访问修饰符，控制成员函数的访问权限：

* **public**：公有成员，可以在类的外部访问。
* **protected**：受保护成员，仅在该类及其派生类中可访问。
* **private**：私有成员，仅在该类内可访问。

#### 4. 成员函数的重载

成员函数可以重载，这意味着可以定义多个同名的成员函数，只要它们的参数类型或数量不同。

**示例：**

```cpp
class MyClass {
public:
    void display(int value) {
        std::cout << "Integer: " << value << std::endl;
    }

    void display(double value) {
        std::cout << "Double: " << value << std::endl;
    }
};

int main() {
    MyClass obj;
    obj.display(5);      // 输出：Integer: 5
    obj.display(3.14);   // 输出：Double: 3.14
    return 0;
}
```

#### 5. 成员函数的调用

可以通过对象调用成员函数，也可以通过类的引用或指针调用。

**示例：**

```cpp
class MyClass {
public:
    void greet() {
        std::cout << "Hello, World!" << std::endl;
    }
};

int main() {
    MyClass obj;
    obj.greet();  // 通过对象调用

    MyClass* ptr = &obj;
    ptr->greet();  // 通过指针调用

    MyClass& ref = obj;
    ref.greet();  // 通过引用调用
    return 0;
}
```

#### 6. 总结

* 成员函数是 C++ 类的重要组成部分，定义了类的行为。
* 可以根据功能分为普通成员函数、常量成员函数和静态成员函数。
* 成员函数的访问权限受访问修饰符的影响。
* 成员函数可以重载，并且可以通过对象、指针和引用进行调用。

成员函数提供了在类内部操作数据成员和实现功能的能力，是 C++ 面向对象编程的核心特性之一。
