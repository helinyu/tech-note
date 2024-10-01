# 函数

### 1. **基本函数定义** <a href="#id-1.-ji-ben-han-shu-ding-yi" id="id-1.-ji-ben-han-shu-ding-yi"></a>

函数由 返回类型、函数名、参数列表 和 函数体 组成

```
xxx

```

* **返回类型**：函数返回的值类型，如 `int`、`void` 等。
* **函数名**：函数的名称，用于调用函数。
* **参数列表**：函数接受的输入参数，可以为空。
* **函数体**：函数执行的代码块。

### 2. **函数声明与定义**

函数声明（也称为函数原型）通常放在程序的顶部或头文件中，提供了函数的签名。函数定义则包含了函数的具体实现。

{% code title="C++" %}
```
// 函数声明
int add(int, int);

// 函数定义
int add(int a, int b) {
    return a + b;
}

int main() {
    std::cout << add(2, 3) << std::endl;
    return 0;
}
```
{% endcode %}



### 3. **函数参数传递** <a href="#id-3.-han-shu-can-shu-chuan-di" id="id-3.-han-shu-can-shu-chuan-di"></a>

* **按值传递**（Pass by Value）：函数接收参数的副本，修改函数内部的参数不会影响原始数据。
* **按引用传递**（Pass by Reference）：函数接收参数的引用，修改函数内部的参数会影响原始数据。
* **按指针传递**（Pass by Pointer）：函数接收指针，修改指针所指向的内存地址会影响原始数据。

### 4. **默认参数** <a href="#id-4.-mo-ren-can-shu" id="id-4.-mo-ren-can-shu"></a>

是否支持默认参数，即在函数定义时可以为参数指定默认值。如果调用时不传递该参数，则使用默认值：\
\


5\. **函数重载**

是否支持函数重载，即可以定义多个具有相同名称但参数不同的函数。编译器会根据调用时传递的参数类型来选择适当的函数版本：



### 6. **内联函数** <a href="#id-6.-nei-lian-han-shu" id="id-6.-nei-lian-han-shu"></a>

内联函数使用 `inline` 关键字，编译器会尝试将函数的调用替换为其函数体，从而避免函数调用的开销。适用于小函数：



### 7. **函数指针(引用)** <a href="#id-8.-han-shu-zhi-zhen" id="id-8.-han-shu-zhi-zhen"></a>

函数指针是指向函数的指针，允许动态地选择和调用函数。函数指针的定义与普通指针类似，只是类型为函数签名：

{% code title="C++" %}
```
int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int main() {
    int (*operation)(int, int);  // 定义函数指针
    operation = add;
    std::cout << operation(3, 4) << std::endl;  // 调用 add

    operation = subtract;
    std::cout << operation(7, 2) << std::endl;  // 调用 subtract
    return 0;
}
```
{% endcode %}



### 8. 匿名函数 <a href="#id-9.-lambda-biao-da-shi" id="id-9.-lambda-biao-da-shi"></a>

**即匿名函数**，允许在代码中定义短小的内联函数。语法类似于函数，但无需显式命名：

```
auto add = [](int a, int b) {
    return a + b;
};

int main() {
    std::cout << add(3, 4) << std::endl;  // 输出 7
    return 0;
}
```

### 9. **模板函数 【不一定有】** <a href="#id-10.-mu-ban-han-shu" id="id-10.-mu-ban-han-shu"></a>

模板函数允许编写通用函数，可以处理多种类型的输入。模板函数通过模板参数定义：

{% code title="C++" %}
```
template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    std::cout << add(3, 4) << std::endl;  // 输出 int 7
    std::cout << add(3.5, 4.2) << std::endl;  // 输出 double 7.7
    return 0;
}
```
{% endcode %}







```ini
函数
1、定义函数的结构是怎么写的？有没有关键字，python-def , js - founction 
2、参数 —— 默认参数（没有传值，使用默认值）、 位置参数（有顺序） 关键参数（可指名道姓的采纳数）、可变参数（常见的...args）
3、作用域（应该不会变）
4、匿名函数、lambda（匿名函数），闭包
5、装饰器，（这个不常见，未来可能很常见）
6、嵌套与递归
```

```ini
匿名函数、lambda 、闭包
lambda 是匿名函数的一种，匿名函数只是为了方便使用，没必要具名的时候就变成了匿名函数
闭包：一个能够引用外部作用域变量的函数，无论它实现是lambda、匿名函数、具名函数都是可以的。
lambda、匿名函数 —— 具体实现
闭包 —— 是一个概念。具体实现可以多样的。
```
