# 共用体

C++中有共用体（union），C++中的共用体与C语言中的共用体大部分特性是相似的，但也存在一些细微的区别：

**一、C++中对共用体的增强**

1.  类型安全：

    * C++中可以使用`union`关键字加上类名的方式定义共用体，并且可以在共用体内部定义成员函数，这使得共用体在一定程度上更加类型安全。
    * 例如：

    ```cpp
    union MyUnion {
        int num;
        double dbl;
        void setNum(int n) { num = n; }
        int getNum() const { return num; }
    };
    ```
2. 命名空间：
   * C++中的共用体是在命名空间范围内定义的，这有助于避免命名冲突。
3. 支持面向对象特性：
   * C++中的共用体可以与类一起使用，支持继承、多态等面向对象特性。例如，可以在类中包含共用体作为成员变量，或者从共用体派生类。

**二、默认访问权限**

* C 语言中，共用体成员的默认访问权限是公共的（public）。
* C++中，共用体成员的默认访问权限也可以是公共的，但如果使用类的方式定义共用体，可以通过指定访问说明符（如`public`、`private`、`protected`）来控制成员的访问权限。

**三、初始化方式**

* C++中可以使用初始化列表对共用体进行初始化，就像对类进行初始化一样。例如：

```cpp
union MyUnion {
    int num;
    double dbl;
};

MyUnion u = {10}; // 初始化共用体的 num 成员为 10
```

总的来说，C++中的共用体在功能上与 C 语言中的共用体类似，但 C++提供了更多的语言特性和灵活性，可以使共用体的使用更加安全和方便。
