# 变量类型

在 C++中，变量类型主要有以下几类：

由于C++中都可以使用C语言的变量类型， C++是C语言的超集，所以，C语言有的，C++都有。



## 下面是C++比C多出来的类型

**1、类类型变量（用户自定义类型）**

通过类定义创建的对象变量。例如：

```cpp
class MyClass {
public:
    int data;
};

MyClass obj;
obj.data = 10;
```



**2、模板类型变量（泛型编程）**

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
