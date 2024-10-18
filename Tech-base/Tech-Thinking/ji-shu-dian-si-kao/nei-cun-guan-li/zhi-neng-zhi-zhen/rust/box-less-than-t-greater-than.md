# Box\<T>

在 Rust 中，`Box<T>` 是一种智能指针类型，专门用于将数据放到堆上进行动态分配。它主要用于以下几种场景： 类似C++中的unique\_ptr指针。

1. **在堆上分配数据**：使用 `Box`，你可以在堆上存储大小固定的数据。对于非常大的结构体，可以避免在栈上占用过多空间。
2. **实现递归数据结构**：Rust 不允许在编译时确定大小的递归类型（例如树、链表），因此 `Box` 允许构建这些数据结构。
3. **类型转换和特征对象**：将结构体或类型转换为特征对象（例如 `dyn Trait`）。

#### 基本用法

1.  **创建和解引用 `Box`**

    ```rust
    fn main() {
        let x = 5;
        let boxed_x = Box::new(x); // 将整数 `5` 放在堆上
        println!("boxed_x: {}", *boxed_x); // 解引用
    }
    ```

    这里 `Box::new(x)` 将整数 `5` 分配在堆上，`*boxed_x` 解引用来获取数据。
2.  **递归数据结构** `Box` 对递归数据结构特别有用，比如链表：

    ```rust
    enum List {
        Node(i32, Box<List>),
        Nil,
    }

    fn main() {
        let list = List::Node(1, Box::new(List::Node(2, Box::new(List::Nil))));
    }
    ```

    使用 `Box<List>` 可以创建一个递归定义的链表结构。
3.  **动态分配和特征对象** `Box` 还可以用于存储实现特定特征的类型：

    ```rust
    trait Draw {
        fn draw(&self);
    }

    struct Circle;
    impl Draw for Circle {
        fn draw(&self) {
            println!("Drawing a circle");
        }
    }

    fn main() {
        let shape: Box<dyn Draw> = Box::new(Circle);
        shape.draw();
    }
    ```

    在这里，`Box<dyn Draw>` 将 `Circle` 转换成一个特征对象 `Draw`，实现了多态性。

#### 性能与内存管理

`Box` 的开销非常小，因为它只是存储了一个指针。它适合在需要堆上分配单个对象时使用，而无需复杂的引用计数或多线程控制。
