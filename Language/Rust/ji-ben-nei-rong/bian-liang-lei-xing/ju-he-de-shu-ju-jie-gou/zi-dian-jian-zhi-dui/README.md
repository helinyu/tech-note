# 字典/键值对

Dictionary/Map 这个是标准的字典形式

对象 ： 因为对象有属性值的关系，无形中就是key/value的形式，可以转化为对应的内容。



在 Rust 中，`Map` 通常指的是哈希映射（`HashMap`），是一个存储键值对的集合。`HashMap` 使用哈希表实现，允许快速查找、插入和删除操作。

#### 1. **Rust 中的 HashMap 内容**

**创建 HashMap**

需要引入标准库的 `std::collections` 模块。

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

**特性**

* **键唯一性**：每个键都是唯一的，插入重复键时会覆盖原有值。
* **动态大小**：可以在运行时添加或删除键值对。
* **无序存储**：键值对的存储顺序不是固定的，遍历时可能以不同的顺序返回。

#### 2. **与其他语言的 Map 比较**

| 特性       | Rust HashMap              | Java Map                        | Python dict  | C++ std::unordered\_map |
| -------- | ------------------------- | ------------------------------- | ------------ | ----------------------- |
| **键类型**  | 支持任何实现了 `Hash` 和 `Eq` 的类型 | 支持任何对象类型                        | 支持任何不可变的哈希对象 | 支持任何实现了 `Hash` 的类型      |
| **值类型**  | 任意类型                      | 任意对象类型                          | 任意类型         | 任意类型                    |
| **动态大小** | 支持动态大小，随时可以增删             | 支持动态大小                          | 支持动态大小       | 支持动态大小                  |
| **访问方式** | 通过键直接访问                   | 通过键直接访问                         | 通过键直接访问      | 通过键直接访问                 |
| **无序存储** | 无固定顺序                     | 取决于具体实现（如 `HashMap`）            | 无固定顺序        | 无固定顺序                   |
| **线程安全** | 默认不安全，需要外部锁               | 可以使用 `ConcurrentHashMap` 实现线程安全 | 默认不安全        | 默认不安全                   |

#### 3. **总结**

Rust 的 `HashMap` 提供了一种高效的方式来存储和操作键值对，强调类型安全和内存管理。与 Java 的 `Map`、Python 的 `dict` 和 C++ 的 `unordered_map` 相比，Rust 的 `HashMap` 在性能和安全性上具有相似的优势。每种语言的实现都根据其特性有所不同，但都提供了灵活的键值对存储和访问方式。
