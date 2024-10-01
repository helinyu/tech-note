# set 和map

在 Rust 中，`Set` 和 `Map` 数据结构主要由标准库中的 `std::collections` 模块提供。这些集合类型允许存储不重复的值（Set）和键值对（Map），并提供高效的查找、插入和删除操作。

#### 1. **Set（集合）**

`HashSet` 是 Rust 中提供的集合类型，使用哈希表实现，存储不重复的元素。它的主要特点是快速的查找和插入操作。

**创建和使用 `HashSet`：**

```rust
use std::collections::HashSet;

fn main() {
    let mut set = HashSet::new();

    // 插入元素
    set.insert(1);
    set.insert(2);
    set.insert(3);
    set.insert(2);  // 插入重复的元素，不会添加

    // 检查是否包含某个元素
    if set.contains(&2) {
        println!("集合中包含元素 2");
    }

    // 遍历集合
    for value in &set {
        println!("{}", value);
    }

    // 移除元素
    set.remove(&1);
}
```

**特点：**

* **不重复**：`HashSet` 只存储唯一值，插入重复值不会导致错误，但会被忽略。
* **哈希表实现**：提供 O(1) 的平均时间复杂度用于插入、删除和查找操作。
* **无序**：元素的存储顺序不是固定的，遍历时可能会以不同的顺序返回元素。

#### 2. **Map（映射）**

`HashMap` 是 Rust 中的键值对存储类型，允许通过键来快速查找值。它也使用哈希表实现。

**创建和使用 `HashMap`：**

```rust
use std::collections::HashMap;

fn main() {
    let mut map = HashMap::new();

    // 插入键值对
    map.insert("apple", 3);
    map.insert("banana", 2);
    map.insert("orange", 5);

    // 访问值
    if let Some(&count) = map.get("apple") {
        println!("苹果的数量: {}", count);
    }

    // 遍历键值对
    for (key, value) in &map {
        println!("{}: {}", key, value);
    }

    // 移除键值对
    map.remove("banana");
}
```

**特点：**

* **键值对**：`HashMap` 存储键值对，每个键都是唯一的。
* **哈希表实现**：提供 O(1) 的平均时间复杂度用于插入、删除和查找操作。
* **无序**：键值对的存储顺序不是固定的，遍历时可能会以不同的顺序返回。

#### 3. **总结**

Rust 提供的集合类型 `HashSet` 和 `HashMap` 是高效的容器，适用于存储不重复的元素和键值对。它们使用哈希表实现，支持快速的查找和修改操作，适合处理需要频繁插入和查询的场景。由于它们是无序的，在使用时要注意元素的顺序问题。
