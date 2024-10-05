# C++上的多态

在 C++ 中，多态（Polymorphism）同样是面向对象编程中的重要概念。C++ 支持两种形式的多态：**编译时多态**和**运行时多态**。

#### 1. 编译时多态（静态多态）

编译时多态是在编译期间决定调用的函数实现，主要通过**函数重载**（Function Overloading）和**运算符重载**（Operator Overloading）来实现。

**函数重载示例：**

```cpp
#include <iostream>

class Math {
public:
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
};

int main() {
    Math math;
    std::cout << math.add(5, 3) << std::endl;       // 输出：8
    std::cout << math.add(2.5, 1.5) << std::endl;   // 输出：4.0
    return 0;
}
```

在上面的代码中，`add` 函数被重载了两次，根据传递的参数类型，编译器决定调用哪一个 `add` 函数。

**运算符重载示例：**

```cpp
#include <iostream>

class Complex {
public:
    int real, imag;

    Complex(int r = 0, int i = 0) : real(r), imag(i) {}

    Complex operator + (const Complex &other) {
        return Complex(real + other.real, imag + other.imag);
    }
};

int main() {
    Complex c1(3, 2), c2(1, 7);
    Complex c3 = c1 + c2;
    std::cout << "Real: " << c3.real << ", Imag: " << c3.imag << std::endl;
    return 0;
}
```

这里重载了加法运算符 `+`，使得它能够处理 `Complex` 类的对象。

#### 2. 运行时多态（动态多态）

运行时多态主要通过**继承**和**虚函数**（Virtual Functions）实现。当使用基类指针或引用指向派生类对象时，调用虚函数可以根据对象的实际类型执行不同的行为。这是在程序运行时根据对象的动态类型决定调用哪个函数实现。

**示例：**

```cpp
#include <iostream>

class Animal {
public:
    virtual void speak() {
        std::cout << "Animal makes a sound" << std::endl;
    }
};

class Dog : public Animal {
public:
    void speak() override {
        std::cout << "Dog barks" << std::endl;
    }
};

class Cat : public Animal {
public:
    void speak() override {
        std::cout << "Cat meows" << std::endl;
    }
};

int main() {
    Animal* animal;
    Dog dog;
    Cat cat;

    animal = &dog;
    animal->speak();  // 输出：Dog barks

    animal = &cat;
    animal->speak();  // 输出：Cat meows

    return 0;
}
```

**虚函数与多态：**

在这个例子中，`Animal` 类有一个虚函数 `speak`。当通过 `Animal` 的指针 `animal` 调用 `speak` 函数时，根据对象的实际类型（`Dog` 或 `Cat`），会调用各自的 `speak` 函数。这就是运行时多态的核心。

**关键点：**

1. **虚函数**：必须在基类中将函数声明为 `virtual`，以便在派生类中实现多态。
2. **覆盖（override）**：派生类可以重写基类的虚函数，实现不同的行为。
3. **基类指针或引用**：多态通常通过基类的指针或引用来调用派生类的重写方法。

#### 总结

* **编译时多态**：通过函数重载和运算符重载实现，编译期间决定调用哪一个函数。
* **运行时多态**：通过继承和虚函数实现，运行时根据对象的动态类型调用合适的方法。

C++ 的多态特性极大地增强了代码的可扩展性和灵活性。
