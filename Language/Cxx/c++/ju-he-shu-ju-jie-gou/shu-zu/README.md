# 数组

#### C++中的数组

C++中的数组与C中的数组非常相似，但C++提供了一些额外的功能：

1.  **声明与初始化**\
    声明和初始化与C语言基本相同：

    ```cpp
    int arr[5] = {1, 2, 3, 4, 5};  // 静态数组的初始化
    ```
2. **STL中的数组**\
   C++提供了`std::array`和`std::vector`来克服C风格数组的限制：
   *   `std::array`：用于固定大小的数组，它是模板类，数组大小是编译时常量。

       ```cpp
       #include <array>
       std::array<int, 5> arr = {1, 2, 3, 4, 5};  // 声明并初始化
       ```

       该数组支持标准容器接口，例如`size()`：

       ```cpp
       size_t size = arr.size();
       ```
   *   `std::vector`：支持动态调整大小的数组，可以在运行时添加或删除元素。

       ```cpp
       #include <vector>
       std::vector<int> vec = {1, 2, 3, 4, 5};
       vec.push_back(6);  // 添加新元素
       ```
3.  **数组的范围循环（Range-based for loop）**\
    在C++11及更高版本中，可以使用范围循环轻松遍历数组：

    ```cpp
    for (int x : arr) {
        std::cout << x << std::endl;
    }
    ```

#### 总结

* 在C语言中，数组的大小是固定的，无法动态调整。
* 在C++中，除了使用C风格的数组外，还可以使用`std::array`（固定大小）和`std::vector`（动态大小）来处理数组，提供了更多的灵活性和功能。
