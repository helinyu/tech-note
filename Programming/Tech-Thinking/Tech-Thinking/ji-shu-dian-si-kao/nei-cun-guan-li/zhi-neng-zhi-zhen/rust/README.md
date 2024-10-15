# Rust

Rust 中的智能指针通过封装指针和提供额外功能来增强内存管理。常见的智能指针包括：

1. **Box\<T>**：最简单的智能指针，用于在堆上分配内存，并拥有唯一的所有权。适用于静态大小不确定的数据类型或递归类型。
2. **Rc\<T>**（Reference Counted）：一种引用计数智能指针，用于共享内存所有权。适合单线程场景，但无法用于可变数据，因为它不支持内部可变性。
3. **Arc\<T>**（Atomic Reference Counted）：与 `Rc` 类似，但通过原子操作实现线程安全的引用计数，可以在多线程环境中使用。
4. **RefCell\<T>**：允许在运行时检查借用规则，而不是编译时。通过内部可变性（interior mutability）提供可变借用，用于需要共享但又希望可变的场景。
5. **Cell\<T>**：与 `RefCell` 类似，也提供内部可变性，但其 API 仅限于 Copy 类型的数据，适合需要原子地读取和写入的简单值。
6. **Mutex\<T>** 和 **RwLock\<T>**：分别用于在多线程场景中实现互斥锁和读写锁。`Mutex` 提供互斥访问，`RwLock` 允许多个读或一个写访问。
7. **Weak\<T>**：与 `Rc` 或 `Arc` 配合使用，创建不增加引用计数的弱引用。防止循环引用导致内存泄漏，适合需要缓存或管理生命周期的场景。

#### 示例

```rust
use std::rc::Rc;
use std::cell::RefCell;

struct Node {
    value: i32,
    next: Option<Rc<RefCell<Node>>>,
}

fn main() {
    let node1 = Rc::new(RefCell::new(Node { value: 1, next: None }));
    let node2 = Rc::new(RefCell::new(Node { value: 2, next: Some(node1.clone()) }));
    node1.borrow_mut().next = Some(node2.clone()); // 循环引用
}
```

这里我们用 `Rc<RefCell<T>>` 创建了双向引用链表，通过 `Weak` 可以解决循环引用问题。
