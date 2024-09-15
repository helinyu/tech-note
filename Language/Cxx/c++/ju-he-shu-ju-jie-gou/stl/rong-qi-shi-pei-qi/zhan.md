# 栈

`std::stack` 是 C++ STL 中的容器适配器，它提供了一个**栈**的数据结构，即**后进先出**（LIFO）的操作方式。栈的主要操作是插入元素到栈顶、移除栈顶元素，以及访问栈顶元素。它基于其他序列式容器（如 `std::deque` 或 `std::vector`）实现。

## 1. **构造函数**

* **默认构造函数**：
  * `std::stack<T>`：创建一个空的栈，`T` 是栈中元素的数据类型。
* **带容器的构造函数**：
  * `std::stack<T, Container>`：创建一个指定底层容器的栈，`Container` 是底层的具体容器类型，默认是 `std::deque<T>`。

## 2. **属性**

**类型定义**

* `value_type`：栈中元素的类型。
* `container_type`：底层容器的类型（默认为 `std::deque<T>`）。
* `size_type`：栈中元素大小的类型（通常是 `std::size_t`）。
* `reference`：返回元素的引用类型。
* `const_reference`：返回常量元素的引用类型。

## 3. **成员方法**

### **3.1 元素访问**

* **`top()`**：
  * **功能**：返回栈顶元素的引用，不移除元素。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      std::stack<int> s;
      s.push(10);
      s.push(20);
      std::cout << s.top();  // 输出 20# 
      ```

### **3.2 容量相关**

* **`empty()`**：
  * **功能**：检查栈是否为空，如果栈为空返回 `true`，否则返回 `false`。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      if (s.empty()) {
          std::cout << "Stack is empty";
      }
      ```
* **`size()`**：
  * **功能**：返回栈中元素的数量。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      std::cout << "Size: " << s.size();  // 输出栈中元素数量
      ```

### **3.3 修改容器**

* **`push(const value_type& val)`**：
  * **功能**：将元素 `val` 压入栈顶。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      s.push(30);  // 将 30 压入栈顶
      ```
* **`emplace(Args&&... args)`**：
  * **功能**：原位构造元素，并将其压入栈顶，避免了额外的复制操作。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      s.emplace(40);  // 原位构造并压入栈顶
      ```
* **`pop()`**：
  * **功能**：移除栈顶元素。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      s.pop();  // 移除栈顶元素
      ```

### **3.4 交换内容**

* **`swap(stack& other)`**：
  * **功能**：与另一个栈 `other` 交换元素。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      std::stack<int> s1, s2;
      s1.push(10);
      s2.push(20);
      s1.swap(s2);  // 交换两个栈的内容
      ```

## 4. **示例代码**

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> s;

    // 插入元素
    s.push(10);
    s.push(20);
    s.push(30);

    // 查看栈顶元素
    std::cout << "Top element: " << s.top() << std::endl;  // 输出 30

    // 移除栈顶元素
    s.pop();
    std::cout << "Top element after pop: " << s.top() << std::endl;  // 输出 20

    // 栈的大小
    std::cout << "Size: " << s.size() << std::endl;  // 输出 2

    // 检查栈是否为空
    if (!s.empty()) {
        std::cout << "Stack is not empty" << std::endl;
    }

    return 0;
}
```

## 5. **`std::stack` 的底层容器**

* **默认容器**：`std::stack` 默认使用 `std::deque` 作为底层容器，但也可以使用 `std::vector` 或 `std::list`。
*   **使用 `std::vector`**：

    ```cpp
    std::stack<int, std::vector<int>> s;  // 使用 std::vector 作为底层容器
    ```
*   **使用 `std::list`**：

    ```cpp
    std::stack<int, std::list<int>> s;  // 使用 std::list 作为底层容器
    ```

## 6. **应用场景**

* **括号匹配**：用于检查表达式中的括号是否配对。
* **函数调用栈**：用于保存函数调用的返回地址，实现递归调用。
* **回溯算法**：用于在回溯中保存路径信息。
* **深度优先搜索**：DFS 算法中可以使用栈来模拟递归调用。



## 7. **总结**

| 方法                        | 描述            | 时间复杂度 |
| ------------------------- | ------------- | ----- |
| `top()`                   | 返回栈顶元素的引用。    | O(1)  |
| `push(const T& val)`      | 将元素压入栈顶。      | O(1)  |
| `emplace(Args&&... args)` | 原位构造新元素并压入栈顶。 | O(1)  |
| `pop()`                   | 移除栈顶元素。       | O(1)  |
| `empty()`                 | 检查栈是否为空。      | O(1)  |
| `size()`                  | 返回栈中元素的数量。    | O(1)  |
| `swap(stack& other)`      | 交换两个栈的内容。     | O(1)  |

`std::stack` 是一个简单的容器适配器，适用于需要后进先出（LIFO）操作的场景，比如括号匹配、递归处理、函数调用栈等。
