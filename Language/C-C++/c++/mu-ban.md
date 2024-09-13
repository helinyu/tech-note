# 模板

C++ 中的模板（Template）是一种强大的泛型编程工具，使得函数和类可以处理多种类型的参数，而无需重写代码。模板使得编写通用的代码变得更加灵活和高效，广泛应用于标准模板库（STL）中。

C++ 中有两种主要的模板：

1. **函数模板（Function Template）**
2. **类模板（Class Template）**

## 1. **函数模板**

函数模板允许你编写通用的函数，不需要为不同的数据类型重复编写函数。编译器在使用时根据传递的参数类型生成相应的函数实例。

### **1.1 定义和使用函数模板**

```cpp
template <typename T>
T add(T a, T b) {
    return a + b;
}
```

* `template <typename T>`：表示声明一个模板，`T` 是占位符类型，可以是任意数据类型。
* `T add(T a, T b)`：这是一个返回类型为 `T` 的函数，参数类型也都是 `T`，可以传递任何类型的参数，只要支持 `+` 运算符。

&#x20;**示例**

```cpp
#include <iostream>
using namespace std;

template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    int x = 10, y = 20;
    double a = 1.5, b = 2.5;

    // 使用模板函数
    cout << "add(x, y) = " << add(x, y) << endl;   // 整数加法
    cout << "add(a, b) = " << add(a, b) << endl;   // 浮点数加法

    return 0;
}
```

### **1.2 函数模板的类型推导**

编译器可以根据传递的参数类型自动推导模板类型：

```cpp
cout << add(3, 4);     // 推导为 int
cout << add(1.2, 3.4); // 推导为 double
```

## 2. **类模板**

类模板允许你为多个数据类型设计通用的类，而不需要针对每种类型编写不同的类。

### **2.1 定义和使用类模板**

```cpp
template <typename T>
class Box {
private:
    T value;
public:
    Box(T val) : value(val) {}
    T getValue() { return value; }
};
```

* `template <typename T>`：定义一个模板类，`T` 是占位符类型。
* `Box<T>`：表示一个泛型类，`T` 可以是任何类型，类中的成员变量 `value` 和方法 `getValue()` 都使用类型 `T`。

**示例**

```cpp
#include <iostream>
using namespace std;

template <typename T>
class Box {
private:
    T value;
public:
    Box(T val) : value(val) {}
    T getValue() { return value; }
};

int main() {
    Box<int> intBox(123);       // 创建存储 int 类型的对象
    Box<double> doubleBox(456.78);  // 创建存储 double 类型的对象

    cout << "intBox: " << intBox.getValue() << endl;
    cout << "doubleBox: " << doubleBox.getValue() << endl;

    return 0;
}
```

输出：

```
intBox: 123
doubleBox: 456.78
```

## 3. **模板的特化**

模板特化<mark style="color:orange;">**允许你为特定的数据类型提供特定的实现，而不使用通用的模板版本**</mark>。这在某些类型有特殊处理需求时非常有用。

### **3.1 函数模板特化**

```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

// 针对 const char* 类型的特化
template <>
const char* max<const char*>(const char* a, const char* b) {
    return (strcmp(a, b) > 0) ? a : b;
}
```

### **3.2 类模板特化**

```cpp
template <typename T>
class Box {
private:
    T value;
public:
    Box(T val) : value(val) {}
    T getValue() { return value; }
};

// 针对 int 类型的特化
template <>
class Box<int> {
private:
    int value;
public:
    Box(int val) : value(val) {}
    int getValue() { return value * 2; }  // 针对 int 类型的特殊处理
};
```

## 4. **模板的部分特化**

类模板还可以进行**部分特化**，即对某些特定类型进行定制化处理，而保留其他类型的通用性。

```cpp
template <typename T, typename U>
class Pair {
public:
    T first;
    U second;
    Pair(T f, U s) : first(f), second(s) {}
};

// 对第二个类型是 int 的部分特化
template <typename T>
class Pair<T, int> {
public:
    T first;
    int second;
    Pair(T f, int s) : first(f), second(s) {}
};
```

## 5. **模板的应用场景**

* **泛型编程**：模板使得编写通用的函数和类成为可能，避免了重复代码。
* **容器类**：C++ 标准模板库（STL）中的容器类（如 `std::vector`、`std::map`、`std::list`）和算法都基于模板实现，能够处理不同类型的数据。
* **算法库**：通过模板，算法可以适用于多种数据类型而无需修改实现。



## 6. **模板与内联**

模板代码一般在头文件中定义，原因是模板代码只有在使用时才会生成实际的函数或类，因此编译器需要在使用模板时知道其定义。

## 7. **模板的编译过程**

模板在编译时会进行两步检查：

1. **模板定义检查**：编译器检查模板语法是否正确，但不会生成实际代码。
2. **模板实例化**：当使用模板时，编译器根据具体类型实例化模板并生成实际的函数或类代码。

## 8. **模板的优缺点**

**优点：**

* **代码复用**：通过模板，编写一次代码可以适用于多种数据类型，减少了重复代码。
* **类型安全**：模板提供了类型安全的编程方式，编译时会根据类型进行检查，避免了运行时类型错误。

**缺点：**

* **编译时间增加**：模板代码在使用时才进行实例化，这可能会增加编译时间。
* **代码膨胀**：不同类型的模板实例化会生成不同的代码，这可能导致编译后的代码体积增大。

## 9. **模板的高级特性**

* **模板模板参数**：可以在模板中传递模板作为参数。
* **SFINAE（Substitution Failure Is Not An Error）**：模板替换失败并不会导致编译错误，而是尝试其他的匹配。
* **变参模板（Variadic Templates）**：允许模板接受任意数量的参数。

```cpp
template<typename... Args>
void print(Args... args) {
    (cout << ... << args) << endl;
}
```

#### 总结

**模板是 C++ 中实现泛型编程的核心工具**。通过模板，程序员可以编写通用代码，并为不同类型提供一致的接口，提升了代码的可重用性和灵活性。
