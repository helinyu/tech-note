# 内存管理函数

在 C++ 中，内存分配的方法与 C 有所不同，除了支持 C 中的 `malloc`、`calloc`、`realloc` 和 `free` 外，还引入了面向对象的内存管理方式。以下是 C++ 中常用的内存分配方法：

#### 1. **`new` 运算符**

* 功能：在堆上分配内存，并调用构造函数来初始化对象。适用于单个对象和数组。
* 语法：
  * 分配单个对象：`Type* ptr = new Type;`
  * 分配数组：`Type* ptr = new Type[size];`
* 返回值：返回一个指向新分配内存的指针，如果分配失败会抛出 `std::bad_alloc` 异常。
*   例子：

    ```cpp
    int* p = new int;      // 分配一个整数
    int* arr = new int[10]; // 分配存储 10 个整数的数组
    ```

#### 2. **`delete` 运算符**

* 功能：释放由 `new` 分配的内存，并调用析构函数来清理对象。适用于单个对象和数组。
* 语法：
  * 释放单个对象：`delete ptr;`
  * 释放数组：`delete[] ptr;`
*   例子：

    ```cpp
    delete p;       // 释放单个整数的内存
    delete[] arr;   // 释放数组的内存
    ```

#### 3. **`malloc`、`calloc`、`realloc` 和 `free`**

* C++ 也支持 C 中的这些内存分配函数，不过它们不会调用构造函数或析构函数，因此适用于纯粹的内存管理，而不涉及对象的初始化和清理。
*   例子：

    ```cpp
    int* p = (int*) malloc(sizeof(int));  // 使用 malloc 分配内存
    free(p);                              // 使用 free 释放内存
    ```

#### 4. **智能指针（`std::unique_ptr` 和 `std::shared_ptr`）**

* 功能：C++ 标准库中提供了智能指针，用于自动管理内存，避免手动调用 `delete`，降低内存泄漏的风险。
* 语法：
  * `std::unique_ptr<Type> ptr = std::make_unique<Type>();`
  * `std::shared_ptr<Type> ptr = std::make_shared<Type>();`
*   例子：

    ```cpp
    #include <memory>

    std::unique_ptr<int> p = std::make_unique<int>(10);  // 创建一个 unique_ptr
    std::shared_ptr<int> sp = std::make_shared<int>(20); // 创建一个 shared_ptr
    ```

#### 总结：

* **`new` 和 `delete`**：用于动态分配和释放对象，适合需要调用构造和析构函数的场景。
* **`malloc`、`calloc`、`realloc` 和 `free`**：用于传统的 C 风格的内存分配。
* **智能指针**：推荐使用，提供了更安全和方便的内存管理方式。
