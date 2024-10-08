# C++中指针和引用的关系与区别？ 以及& \* 符号，对取地址以及引用的区别

在 C++ 中，**指针**和**引用**是两种用于操作内存地址的机制，它们有一些相似之处，但本质上是不同的。下面是指针和引用的关系、区别以及符号 `&` 和 `*` 的使用解释：

#### 1. 指针和引用的关系与区别

**1.1 指针**

指针是存储 **内存地址** 的变量。它可以指向任何类型的对象或数据类型。指针可以通过解引用（`*`）操作符访问其指向的对象，并且指针本身可以修改来指向不同的对象。

**指针的特点：**

* 指针是一个变量，存储的是某个对象的内存地址。
* 指针可以为空（`nullptr` 或 `NULL`），即指向没有实际对象的地方。
* 指针可以重新赋值，使其指向不同的对象。
* 指针有算术操作，如 `++`、`--`、`+` 等。

```cpp
int x = 10;
int* ptr = &x;  // ptr 存储 x 的地址
std::cout << *ptr;  // 通过解引用访问 x 的值, 输出 10
```

**1.2 引用**

引用是一个对象的别名，创建后引用必须绑定到某个对象，并且 **不能更改**。引用不是独立的对象，它只是原始对象的一个别名，所有对引用的操作实际是对原始对象的操作。

**引用的特点：**

* 引用必须在声明时初始化，且不能重新绑定到其他对象。
* 引用是透明的（像变量的别名），使用起来和原始变量没有区别。
* 引用不可以是空的，它始终引用一个对象。

```cpp
int x = 10;
int& ref = x;  // ref 是 x 的引用
ref = 20;  // 修改 ref 等于修改 x
std::cout << x;  // 输出 20
```

**1.3 指针与引用的区别**

* **初始化**：指针可以在声明后初始化，而引用必须在声明时初始化。
* **重新绑定**：指针可以通过赋值语句重新指向不同的对象，而引用在初始化后不能改变它所绑定的对象。
* **空值**：指针可以为空（`nullptr`），而引用必须始终绑定一个有效的对象。
* **内存占用**：指针占用内存来存储地址，引用没有实际的内存占用，它只是对象的别名。
* **运算操作**：指针支持指针算术操作（如递增、递减等），引用不支持任何运算操作。

#### 2. `&` 和 `*` 符号的含义

**2.1 `&` 符号**

* **取地址符（Address-of Operator）**：在普通变量前使用 `&` 表示取该变量的内存地址。

```cpp
int x = 10;
int* ptr = &x;  // 使用 & 获取 x 的地址
```

* **引用声明符（Reference Operator）**：在变量声明时使用 `&`，表示声明一个引用。

```cpp
int y = 20;
int& ref = y;  // 使用 & 声明引用 ref，引用 y
```

**2.2 `*` 符号**

* **指针解引用符（Dereference Operator）**：在指针前使用 `*` 表示访问指针指向的对象。

```cpp
int* ptr = &x;
int val = *ptr;  // 通过解引用 *ptr 获取 x 的值
```

* **指针声明符（Pointer Declaration）**：在类型前使用 `*` 表示声明一个指针变量。

```cpp
int* ptr;  // 使用 * 声明一个指向 int 类型的指针
```

#### 3. 指针和引用的具体示例

**3.1 指针示例**

```cpp
int a = 5;
int* p = &a;  // p 指向 a 的地址
std::cout << *p << std::endl;  // 输出 a 的值 5
*p = 10;  // 修改 a 的值为 10
std::cout << a << std::endl;  // 输出 10
```

**3.2 引用示例**

```cpp
int b = 15;
int& ref = b;  // ref 是 b 的引用
ref = 20;  // 修改 ref 等于修改 b
std::cout << b << std::endl;  // 输出 20
```

**3.3 指针与引用的对比**

```cpp
int c = 30;
int* ptr = &c;   // 指针存储 c 的地址
int& ref = c;    // 引用作为 c 的别名

std::cout << *ptr << std::endl;  // 解引用指针，输出 30
std::cout << ref << std::endl;   // 直接使用引用，输出 30

*ptr = 40;  // 修改指针指向的值
std::cout << ref << std::endl;   // 引用输出更新后的值，输出 40
```

#### 总结

| 特性          | 指针                | 引用           |
| ----------- | ----------------- | ------------ |
| **是否需要初始化** | 不需要必须初始化          | 声明时必须初始化     |
| **是否可重新绑定** | 可以重新指向其他变量        | 不可以重新绑定      |
| **是否可以为空**  | 可以为空（`nullptr`）   | 不能为空         |
| **使用方式**    | 使用 `*` 进行解引用      | 直接使用         |
| **内存开销**    | 占用内存存储地址          | 不占用额外内存，只是别名 |
| **算术操作**    | 支持指针算术操作          | 不支持算术操作      |
| **常见用法**    | 动态内存分配、数组遍历、函数指针等 | 参数传递、创建别名    |



***

## 小结

<mark style="color:red;">1、指针是指向地址的变量， 变量怎么使用，它就可以怎么使用，它确定了类型是指针类型，专门存储地址的。不可以用来存储其他类型的了， 所以，常见的就是直线对象地址的指针，如果基本数据类型，就需要&来取地址了。</mark>

<mark style="color:red;">2、&在声明变量的时候，是引用，是别名。不占用内存空间</mark>

&#x20;   <mark style="color:red;">如果放在变量前面的时候，它就是去地址的作用。</mark>







