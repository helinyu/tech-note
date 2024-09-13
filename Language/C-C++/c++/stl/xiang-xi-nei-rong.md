# 详细内容

C++ 标准模板库（STL）提供了一组功能强大且通用的容器类，用于存储和操作数据。STL中的容器可以大致分为**序列式容器**、**关联式容器**和**无序容器**三大类。每种容器都有不同的特点和适用场景。

#### 1. **序列式容器**（Sequence Containers）

序列容器是指存储数据的顺序容器，通常按照插入的顺序存储数据。这类容器包括常见的数组、链表和双端队列等。

**1.1 `std::vector`**

* **简介**：`std::vector` 是动态数组，支持快速随机访问，动态扩展。
* **特性**：可以动态调整大小、快速访问和插入删除元素（末尾）。
* **适用场景**：频繁的随机访问，少量的中间插入或删除。

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};
vec.push_back(6);
```

**1.2 `std::deque`（双端队列）**

* **简介**：双端队列，支持快速在头部和尾部插入和删除元素。
* **特性**：支持双向插入删除，类似于双端数组。
* **适用场景**：需要频繁在头部和尾部操作元素。

```cpp
std::deque<int> deq = {1, 2, 3};
deq.push_front(0);  // 在前端插入
deq.push_back(4);   // 在后端插入
```

**1.3 `std::list`（双向链表）**

* **简介**：双向链表，元素存储在非连续的内存空间，支持快速的插入和删除操作。
* **特性**：不支持随机访问，但支持快速的头部和中间插入删除。
* **适用场景**：需要频繁进行中间插入和删除操作，不要求随机访问。

```cpp
std::list<int> lst = {1, 2, 3, 4};
lst.push_back(5);  // 在尾部插入
lst.push_front(0); // 在头部插入
```

**1.4 `std::forward_list`（单向链表）**

* **简介**：单向链表，只能在前向方向遍历。
* **特性**：比双向链表更轻量，但不能双向遍历或随机访问。
* **适用场景**：需要较轻量级的链表结构，主要进行前向操作。

```cpp
std::forward_list<int> f_list = {1, 2, 3};
f_list.push_front(0); // 在头部插入
```

**1.5 `std::array`（C++11）**

* **简介**：封装了C风格的静态数组，大小固定。
* **特性**：大小在编译时确定，支持随机访问和STL接口。
* **适用场景**：需要一个大小固定的数组，但希望拥有STL的接口。

```cpp
std::array<int, 5> arr = {1, 2, 3, 4, 5};
```

#### 2. **关联式容器**（Associative Containers）

关联容器基于**平衡二叉树**（通常是红黑树）实现，内部元素会自动排序。

**2.1 `std::set`**

* **简介**：集合，存储唯一的元素，元素自动排序。
* **特性**：自动排序，不能存储重复元素，查找、插入、删除的时间复杂度为O(log n)。
* **适用场景**：需要存储唯一且有序的元素集合。

```cpp
std::set<int> s = {3, 1, 4, 2};
s.insert(5); // 插入元素，自动排序
```

**2.2 `std::multiset`**

* **简介**：与`std::set`类似，但允许存储重复的元素。
* **特性**：自动排序，允许重复元素，操作复杂度同`std::set`。
* **适用场景**：需要存储有序且允许重复的元素集合。

```cpp
std::multiset<int> ms = {1, 3, 1, 4};
```

**2.3 `std::map`**

* **简介**：键值对的有序映射，基于键排序，类似于字典。
* **特性**：键唯一且自动排序，操作复杂度为O(log n)。
* **适用场景**：需要基于键值对存储有序的元素。

```cpp
std::map<int, std::string> mp;
mp[1] = "one";
mp[2] = "two";
```

**2.4 `std::multimap`**

* **简介**：与`std::map`类似，但允许多个相同的键。
* **特性**：允许重复的键，自动排序。
* **适用场景**：需要存储多个相同键的键值对。

```cpp
std::multimap<int, std::string> mmap;
mmap.insert({1, "one"});
mmap.insert({1, "first"});
```

#### 3. **无序容器**（Unordered Containers）

无序容器基于**哈希表**实现，元素存储顺序不固定，但提供平均O(1)的查找、插入、删除时间复杂度。

**3.1 `std::unordered_set`**

* **简介**：无序集合，元素不按顺序存储。
* **特性**：不允许重复元素，基于哈希表，查找、插入和删除平均复杂度为O(1)。
* **适用场景**：对存储顺序无要求，但需要快速查找和唯一性元素的集合。

```cpp
std::unordered_set<int> uset = {3, 1, 4, 2};
```

**3.2 `std::unordered_multiset`**

* **简介**：与`unordered_set`类似，但允许存储重复元素。
* **特性**：允许重复元素，基于哈希表实现。
* **适用场景**：需要存储无序且允许重复的元素。

```cpp
std::unordered_multiset<int> umset = {1, 1, 2, 3};
```

**3.3 `std::unordered_map`**

* **简介**：无序键值对映射，基于哈希表实现。
* **特性**：键唯一，基于哈希表，提供平均O(1)的操作时间。
* **适用场景**：需要无序存储键值对且要求快速查找。

```cpp
std::unordered_map<int, std::string> umap;
umap[1] = "one";
umap[2] = "two";
```

**3.4 `std::unordered_multimap`**

* **简介**：与`unordered_map`类似，但允许多个相同的键。
* **特性**：允许重复键，基于哈希表实现。
* **适用场景**：需要无序存储多个相同键的键值对。

```cpp
std::unordered_multimap<int, std::string> ummap;
ummap.insert({1, "one"});
ummap.insert({1, "first"});
```

#### 3. **容器适配器**（Container Adapters）

容器适配器是对已有容器的封装，提供不同的接口来实现特定的数据结构。

**4.1 `std::stack`**

* **简介**：栈，后进先出（LIFO）数据结构，基于其他容器（如`deque`或`vector`）实现。
* **特性**：只允许在顶端插入和删除元素。
* **适用场景**：需要后进先出的数据结构。

```cpp
std::stack<int> stk;
stk.push(1);
stk.pop();
```

**4.2 `std::queue`**

* **简介**：队列，先进先出（FIFO）数据结构，基于其他容器实现。
* **特性**：只允许在尾部插入，在头部删除元素。
* **适用场景**：需要先进先出的数据结构。

```cpp
std::queue<int> q;
q.push(1);
q.pop();
```

**4.3 `std::priority_queue`**

* **简介**：优先队列，元素按优先级排序，默认大顶堆。
* **特性**：优先级最高的元素在队列前面。
* **适用场景**：需要根据优先级处理元素。

```cpp
std::priority_queue<int> pq;
pq.push(10);
pq.push(5);
pq.push(20);
```



## 总结

C++ STL 提供的容器类可以大致分为以下三大类：

### 1. **序列式容器**（Sequence Containers）

这些容器用于按顺序存储和访问元素，顺序可以是插入时的顺序或指定的顺序。常见的序列式容器有：

* `std::vector`：动态数组，支持随机访问，大小可动态调整。
* `std::deque`：双端队列，支持在头尾两端快速插入和删除元素。
* `std::list`：双向链表，支持快速插入和删除，但不支持随机访问。
* `std::forward_list`：单向链表，仅支持单向遍历和快速插入删除。
* `std::array`：静态数组，大小固定，支持随机访问。

### 2. **关联式容器**（Associative Containers）

#### 1.有序

这些容器基于平衡二叉树（通常是红黑树）实现，元素根据键值自动排序，操作的时间复杂度通常为 O(log n)。常见的关联式容器有：

* `std::set`：集合，存储唯一且有序的元素。
* `std::multiset`：集合，允许存储重复的元素。
* `std::map`：键值对映射，键唯一且自动排序。
* `std::multimap`：键值对映射，允许键重复。

#### **2. 无序**（Unordered Containers）

无序容器基于哈希表实现，元素的存储顺序不固定，查找、插入和删除的平均时间复杂度为 O(1)。常见的无序容器有：

* `std::unordered_set`：无序集合，存储唯一的元素，基于哈希表。
* `std::unordered_multiset`：无序集合，允许存储重复的元素。
* `std::unordered_map`：无序映射，键唯一，基于哈希表。
* `std::unordered_multimap`：无序映射，允许键重复。

### 3. **容器适配器**（Container Adapters）

容器适配器是对现有容器的封装，提供不同的接口以实现特定的数据结构。常见的容器适配器有：

* `std::stack`：栈，后进先出（LIFO）数据结构。
* `std::queue`：队列，先进先出（FIFO）数据结构。
* `std::priority_queue`：优先队列，元素按优先级顺序排列。

这些容器提供了不同的功能和适用场景，帮助程序员根据需求选择合适的数据结构。

{% hint style="info" %}
注意：关联式

1、C++中的map 和set关联是有序的， 如果是没有序的会有unordered前缀

2、set和map的key是唯一的，如果不唯一，会有`multiset前缀的。`

`3、其实关联的容器就是map和set`
{% endhint %}



{% hint style="info" %}
注意：序列式

1、Array 静态数组

2、verctor动态数组

3、deque 双向队列

4、list 双向链表

5、forward\_list 单向链表
{% endhint %}



{% hint style="info" %}
注意：容器适配器

stack 栈

queue 队列

priority\_queue 优先队列
{% endhint %}



## 再次总结：

{% hint style="info" %}
1、数组 vector ，array

2、双向队列 deque

3、链表 list forward\_list

4、映射 map

5、set 集合

6、stack 栈

7、queue队列

8、priority\_queue优先队列
{% endhint %}
