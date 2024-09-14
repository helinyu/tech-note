# 类(对象)

在 C++ 中，\*\*类（Class）**和**对象（Object）\*\*是面向对象编程的核心概念。类是对象的蓝图，定义了对象的属性和行为，而对象是类的实例，拥有类所定义的属性和功能。以下是对 C++ 中类和对象的详细解释。

## 1. **类的基本概念**

**类**是用户定义的类型，包含**数据成员（属性）和成员函数（方法）**。数据成员用于存储对象的状态，成员函数定义了对象的行为。通过定义类，程序员可以创建自己的数据类型，像使用内置类型一样使用这些自定义类型。

**类的基本语法**

```cpp
class ClassName {
public:
    // 构造函数
    ClassName();
    
    // 成员函数（方法）
    void someMethod();
    
    // 数据成员（属性）
    int someAttribute;

private:
    // 私有数据成员和方法
    int privateAttribute;
};
```

* **`class`** 关键字用于定义类。
* **`public`** 和 **`private`** 是访问控制修饰符，控制类成员的可见性。
  * **`public`**：在类外部可以访问的成员。
  * **`private`**：只能在类内部访问的成员，默认情况下，类的成员都是私有的。

## 2. **对象的基本概念**

**对象**是类的实例化，表示具体的实体。一个类可以创建多个对象，每个对象都有自己的一组数据成员值。对象通过使用类中的成员函数来执行操作。

**对象的创建和使用**

```cpp
ClassName obj;  // 创建对象 obj
obj.someMethod();  // 调用对象的方法
obj.someAttribute = 10;  // 访问对象的属性
```

## 3. **类的成员**

### **3.1 数据成员（属性）**

数据成员用于定义类的状态，可以是基本数据类型或其他对象。

```cpp
class Car {
public:
    string brand;  // 公有数据成员
    int year;
};
```

### **3.2 成员函数（方法）**

成员函数是类中定义的函数，用来操作类的数据成员。

```cpp
class Car {
public:
    string brand;
    int year;

    // 成员函数
    void displayInfo() {
        cout << "Brand: " << brand << ", Year: " << year << endl;
    }
};
```

### **3.3 构造函数**

构造函数是一个特殊的成员函数，在对象创建时自动调用，用于初始化对象的状态。构造函数的名字与类名相同，没有返回类型。

```cpp
class Car {
public:
    string brand;
    int year;

    // 构造函数
    Car(string b, int y) {
        brand = b;
        year = y;
    }

    void displayInfo() {
        cout << "Brand: " << brand << ", Year: " << year << endl;
    }
};
```

使用构造函数创建对象：

```cpp
Car myCar("Toyota", 2021);
myCar.displayInfo();
```

### **3.4 析构函数**

析构函数是另一个特殊的成员函数，在对象销毁时自动调用，用于释放资源。析构函数的名字是类名前加 `~`，没有参数，也没有返回值。

```cpp
class Car {
public:
    Car() {
        cout << "Car object created" << endl;
    }

    ~Car() {
        cout << "Car object destroyed" << endl;
    }
};
```

### **3.5 静态成员**

静态成员属于类本身，而不是某个特定的对象。<mark style="color:red;">静态成员在所有对象之间共享。</mark>

*   **静态数据成员**：需要在类外部进行初始化。

    ```cpp
    class Car {
    public:
        static int carCount;  // 静态成员
    };

    int Car::carCount = 0;  // 类外初始化静态成员
    ```
*   **静态成员函数**：只能访问静态成员。

    ```cpp
    class Car {
    public:
        static int carCount;

        static void showCarCount() {
            cout << "Car count: " << carCount << endl;
        }
    };
    ```

## 4. **访问控制**

C++ 提供了三种访问控制修饰符：`public`、`private` 和 `protected`，用于控制类成员的可见性。

* **`public`**：类外部和类内部都可以访问。
* **`private`**：只能在类的内部访问，类外部无法直接访问。
* **`protected`**：与 `private` 类似，但子类可以访问。

```cpp
class Car {
private:
    string brand;
public:
    void setBrand(string b) {
        brand = b;
    }

    string getBrand() {
        return brand;
    }
};
```

在上述示例中，`brand` 是私有的，不能直接从类外访问，只能通过 `setBrand` 和 `getBrand` 这样的公有函数访问。

## 5. **继承**

**继承**允许一个类从另一个类继承数据成员和成员函数。被继承的类称为**基类**，继承的类称为**派生类**。

```cpp
class Vehicle {
public:
    int speed;
    void setSpeed(int s) {
        speed = s;
    }
};

// 派生类 Car 继承自基类 Vehicle
class Car : public Vehicle {
public:
    string brand;
    void setBrand(string b) {
        brand = b;
    }
};
```

通过继承，派生类 `Car` 继承了 `Vehicle` 类的成员函数 `setSpeed` 和数据成员 `speed`。

## 6. **多态**

C++ 中的多态性可以通过**虚函数**来实现，允许在父类中定义的函数在子类中重新定义。

```cpp
class Animal {
public:
    virtual void sound() {
        cout << "Some generic animal sound" << endl;
    }
};

class Dog : public Animal {
public:
    void sound() override {  // 重写父类的 sound 函数
        cout << "Woof!" << endl;
    }
};
```

使用多态调用函数时，可以通过基类的指针或引用来调用派生类的重写版本：

```cpp
Animal* myAnimal = new Dog();
myAnimal->sound();  // 输出: Woof!
```

## 7. **封装**

**封装**是将类的实现细节隐藏起来，只暴露必要的接口给外部，用户通过接口操作对象，而不需要知道内部实现。这通过使用访问控制修饰符来实现，如 `private` 和 `public`。

```cpp
class BankAccount {
private:
    double balance;  // 私有数据成员

public:
    // 通过公有成员函数操作私有数据
    void deposit(double amount) {
        balance += amount;
    }

    double getBalance() {
        return balance;
    }
};
```

## 8. **抽象**

**抽象**是一种表示通用行为的方式，通常使用<mark style="color:orange;">抽象类来实现。抽象类包含纯虚函数，这些函数在基类中没有实现，派生类需要提供实现。</mark>

```cpp
class Shape {
public:
    virtual void draw() = 0;  // 纯虚函数
};

class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a circle" << endl;
    }
};
```

`Shape` 类是一个抽象类，不能实例化，只能通过派生类来实现。

#### 总结

* **类**是对象的模板或蓝图，定义了数据和行为。
* **对象**是类的实例，具有类的所有属性和方法。
* 通过类和对象，C++ 提供了实现面向对象编程的核心机制，包括<mark style="color:red;">**封装、继承、多态和抽象**</mark>。

