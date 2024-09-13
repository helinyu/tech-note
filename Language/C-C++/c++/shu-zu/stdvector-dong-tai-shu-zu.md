# std::vector 动态数组

在 C++中，`std::vector`是一个非常常用的容器，它实现了动态数组的功能。

## **一、主要特点**

1. **动态大小**：可以根据需要自动增长或收缩大小。这使得在运行时可以方便地添加或删除元素，而无需担心数组大小的限制。
2. **高效的随机访问**：支持随机访问迭代器，可以在常量时间内访问任意元素。这使得`std::vector`在需要频繁随机访问元素的场景下非常高效。
3. **内存管理**：自动管理内存，当元素数量增加时，会自动分配更多的内存空间。当元素数量减少时，可能会释放一些不必要的内存以节省空间。
4. **丰富的成员函数**：提供了许多方便的成员函数，**如`push_back`（在末尾添加元素）、`pop_back`（删除末尾元素）、`size`（获取元素数量）、`resize`（调整容器大小）等**。

## **二、基本用法**

1.  **定义和初始化**：

    ```cpp
    std::vector<int> vec1; // 空向量
    std::vector<int> vec2 = {1, 2, 3, 4, 5}; // 初始化列表
    std::vector<int> vec3(10, 5); // 10 个值为 5 的元素
    ```
2.  **添加元素**：

    ```cpp
    vec1.push_back(6); 、
    vec1.push_back(7);
    ```
3.  **访问元素**：

    ```cpp
    int firstElement = vec2[0];
    int secondElement = vec2.at(1);
    ```
4.  **遍历**：

    ```cpp
    // 使用迭代器
    for (auto it = vec3.begin(); it!= vec3.end(); ++it) {
        std::cout << *it << " ";
    }

    // 使用范围 for 循环
    for (int element : vec2) {
        std::cout << element << " ";
    }
    ```
5.  **获取大小**：

    ```cpp
    std::size_t size = vec1.size();
    ```
6.  **调整大小**：

    ```cpp
    vec1.resize(8); // 将向量大小调整为 8
    ```

## **三、与其他容器的转换**

1.  转换为 C 风格数组：

    ```cpp
    int* arr = vec2.data();
    ```

## 四、属性和方法：

**一、属性**

1. 动态大小：可以根据需要自动增长或收缩大小。
2. 连续存储：元素在内存中连续存储，提供高效的随机访问。
3. 类型安全：明确指定存储的元素类型。

**二、方法**

1. **构造函数**：
   * `vector()`：默认构造函数，创建一个空的`vector`。
   * `vector( size_type count, const T& value = T() )`：创建一个包含`count`个相同元素的`vector`。
   * `vector( const vector& other )`：复制构造函数，从另一个`vector`创建新的`vector`。
   * `vector( vector&& other )`：移动构造函数，从另一个`vector`移动创建新的`vector`。
   * `vector( InputIt first, InputIt last )`：使用一对迭代器指定的范围创建`vector`。
2. **元素访问**：
   * `operator[]( size_type pos )`：返回指定位置的元素引用，不进行边界检查，速度较快但不安全。
   * `at( size_type pos )`：返回指定位置的元素引用，进行边界检查，如果访问越界会抛出异常。
   * `front()`：返回第一个元素的引用。
   * `back()`：返回最后一个元素的引用。
   * `data()`：返回指向容器中第一个元素的指针，可以用于与 C 风格的函数交互。
3. **容量相关**：
   * `size()`：返回容器中当前的元素个数。
   * `max_size()`：返回容器能容纳的最大元素个数。
   * `capacity()`：返回容器当前分配的存储容量。
   * `empty()`：判断容器是否为空。
   * `reserve( size_type new_cap )`：预分配足够的内存，使容器至少能容纳`new_cap`个元素。
   * `shrink_to_fit()`：请求减少容器的容量以适应其当前大小。
4. **修改器**：
   * `push_back( const T& value )`：在容器末尾添加一个元素。
   * `pop_back()`：删除容器末尾的元素。
   * `insert( iterator pos, const T& value )`：在指定位置插入一个元素。
   * `erase( iterator pos )`：删除指定位置的元素。
   * `erase( iterator first, iterator last )`：删除指定范围内的元素。
   * `clear()`：删除容器中的所有元素。
   * `assign( InputIt first, InputIt last )`：用一个范围的元素替换容器中的现有元素。
   * `assign( size_type count, const T& value )`：用`count`个相同的元素替换容器中的现有元素。
5. **迭代器相关**：
   * `begin()`：返回指向容器中第一个元素的迭代器。
   * `end()`：返回指向容器中最后一个元素后一个位置的迭代器。
   * `cbegin()`：返回指向容器中第一个元素的常量迭代器。
   * `cend()`：返回指向容器中最后一个元素后一个位置的常量迭代器。
   * `rbegin()`：返回指向容器中最后一个元素的反向迭代器。
   * `rend()`：返回指向容器中第一个元素前一个位置的反向迭代器。
   * `crbegin()`：返回指向容器中最后一个元素的常量反向迭代器。
   * `crend()`：返回指向容器中第一个元素前一个位置的常量反向迭代器。
6. **其他**：
   * `resize( size_type count )`：调整容器的大小为`count`个元素。如果当前大小小于`count`，则添加新元素；如果当前大小大于`count`，则删除多余的元素。
   * `resize( size_type count, const T& value )`：调整容器的大小为`count`个元素。如果当前大小小于`count`，则添加新的初始化为`value`的元素；如果当前大小大于`count`，则删除多余的元素。
   * `swap( vector& other )`：交换两个`vector`的内容。



## **五、应用场景**

1. 当需要动态大小的数组时，特别是在不知道元素数量的情况下。
2. 需要高效的随机访问和频繁的添加、删除元素操作时。
3. 与其他标准库组件（如算法、迭代器等）配合使用时。

