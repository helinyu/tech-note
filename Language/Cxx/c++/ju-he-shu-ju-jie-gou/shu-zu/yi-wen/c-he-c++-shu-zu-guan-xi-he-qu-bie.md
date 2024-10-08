# C和C++数组关系和区别

在 C 和 C++中，数组是一种存储相同类型元素的集合数据结构。以下是关于 C 和 C++中数组的介绍：

**一、相同点**

1. 定义和存储方式：
   * 在 C 和 C++中，数组都是一块连续的内存空间，用于存储相同类型的多个元素。
   * 数组的大小在定义时必须确定，并且一旦定义后，其大小不能改变。例如：`int arr[5];`定义了一个包含 5 个整数的数组。
2. 元素访问：
   * 可以通过下标来访问数组中的元素。下标从 0 开始，到数组大小减 1 结束。例如，`arr[0]`表示访问数组`arr`的第一个元素。
3. 作为函数参数传递：
   * 当数组作为函数参数传递时，实际上传递的是数组的首地址。在函数内部，可以通过这个首地址来访问数组的元素。
   * 由于数组在传递时不包含大小信息，通常需要另外一个参数来指定数组的大小。

**二、不同点**

1. 初始化方式：
   *   C：在 C 中，可以在定义数组时进行初始化，也可以在定义后逐个元素进行赋值。例如：

       ```c
       int arr1[5] = {1, 2, 3, 4, 5};
       int arr2[5];
       arr2[0] = 1;
       arr2[1] = 2;
       //...
       ```
   *   C++：C++除了支持 C 中的初始化方式外，还提供了更灵活的初始化方法，如使用列表初始化。例如：

       ```cpp
       int arr1[5] = {1, 2, 3, 4, 5};
       int arr2[5] = {0}; // 将所有元素初始化为 0
       int arr3[] = {1, 2, 3}; // 自动推断数组大小为 3
       ```
2. 动态分配内存：
   *   C：在 C 中，可以使用`malloc`和`free`函数来动态分配和释放数组的内存空间。例如：

       ```c
       int* arr = (int*)malloc(5 * sizeof(int));
       // 使用数组
       free(arr);
       ```
   *   C++：C++中可以使用`new`和`delete`运算符来动态分配和释放数组的内存空间。此外，C++还提供了`std::vector`等容器类，可以更方便地进行动态内存管理。例如：

       ```cpp
       int* arr = new int[5];
       // 使用数组
       delete[] arr;
       ```
3. 安全性：
   * C++相比 C 提供了更多的安全特性。例如，C++中的数组越界访问在运行时可能会触发错误，而在 C 中可能不会被立即检测到，可能导致未定义行为。
4. 支持的特性：
   * C++中的数组可以作为类的成员变量，并且可以在类的构造函数中进行初始化。
   * C++还支持模板，可以定义通用的数组模板，用于存储不同类型的元素。
