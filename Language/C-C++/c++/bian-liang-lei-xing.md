# 变量类型

在 C++中，变量类型主要有以下几类：

由于C++中都可以使用C语言的变量类型， C++是C语言的超集，所以，C语言有的，C++都有。



## 下面是C++比C多出来的类型



`1、bool`类型

C语言本身没有内置的布尔类型，但可以通过引入`<stdbool.h>`库使用布尔类型：

```c
#include <stdbool.h>
bool flag = true;
```

* 布尔类型实际上是整数类型，`true`等于1，`false`等于0。
* 在 C 语言中通常用`int`类型来模拟布尔值，0 表示假，非 0 表示真。

#### **2、引用类型变量**

引用是一个已有对象的别名。例如：

```cpp
int x = 5;
int& ref = x;
```



**3、类类型变量（用户自定义类型）**

通过类定义创建的对象变量。例如：

```cpp
class MyClass {
public:
    int data;
};

MyClass obj;
obj.data = 10;
```



**4、模板类型变量（泛型编程）**

使用模板可以创建适用于不同类型的变量。例如：

```cpp
template <typename T>
class Container {
public:
    T element;
};

Container<int> intContainer;
intContainer.element = 20;
```

**5、异常类型**\
C++ 支持异常处理机制，有一系列与异常相关的类型用于抛出和捕获异常。例如：\
cppCopy

```
try {
    // Some code that might throw an exception.
} catch (const std::exception& e) {
    // Handle the exception.
}
```
