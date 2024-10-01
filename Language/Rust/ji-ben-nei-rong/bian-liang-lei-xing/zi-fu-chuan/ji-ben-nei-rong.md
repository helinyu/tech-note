# 基本内容

在 Rust 中，字符串有两种主要类型：`String` 和字符串切片（`&str`）。它们各自具有不同的特性和用途。下面是对这两种类型的详细说明。

#### 1. **`String` 类型**

`String` 是一个可变的、堆分配的字符串类型。它的大小在运行时可变，适用于需要动态创建或修改字符串的场景。

**特点：**

* **可变性**：可以在创建后修改其内容。
* **堆分配**：`String` 数据存储在堆上，因此其大小在编译时不需要确定。
* **拥有所有权**：`String` 类型拥有其所包含的字符串数据。

**创建和使用示例：**

```rust
fn main() {
    let mut s = String::from("Hello");  // 创建一个新的 String
    s.push_str(", world!");  // 修改字符串内容
    println!("{}", s);  // 输出: Hello, world!
}
```

#### 2. **字符串切片 (`&str`)**

字符串切片是对字符串的一部分的引用，通常用于对字符串的只读访问。它是一个不可变的、固定大小的视图，通常用来表示字符串的一个切片或从 `String` 中借用的部分。

**特点：**

* **不可变性**：字符串切片不能被修改。
* **内存效率**：因为是引用，不会在堆上分配新的内存。
* **视图**：提供对原始字符串数据的视图，不拥有数据。

**使用示例：**

```rust
fn main() {
    let s: &str = "Hello, world!";  // 字符串切片
    println!("{}", s);  // 输出: Hello, world!
    
    let string = String::from("Hello, Rust!");
    let slice: &str = &string[0..5];  // 获取切片
    println!("{}", slice);  // 输出: Hello
}
```

#### 3. **字符串的常用操作**

**3.1. 拼接**

可以使用 `+` 运算符或 `format!` 宏来拼接字符串。

```rust
fn main() {
    let s1 = String::from("Hello, ");
    let s2 = String::from("world!");
    let s3 = s1 + &s2;  // s1 被移动，s2 以引用方式传入
    println!("{}", s3);  // 输出: Hello, world!

    let s4 = format!("{}{}", s1, s2);  // 不移动，返回新的字符串
    println!("{}", s4);  // 输出: Hello, world!
}
```

**3.2. 长度和遍历**

可以使用 `.len()` 方法获取字符串长度，使用 `chars()` 方法遍历字符。

```rust
fn main() {
    let s = String::from("Hello");
    println!("长度: {}", s.len());  // 输出: 长度: 5

    for c in s.chars() {
        println!("{}", c);  // 遍历并打印每个字符
    }
}
```

#### 4. **处理 UTF-8 字符**

Rust 的 `String` 和 `&str` 都是 UTF-8 编码的，因此可以直接处理 Unicode 字符。

```rust
fn main() {
    let s = String::from("你好");
    println!("{}", s);  // 输出: 你好

    let slice: &str = "你好";
    println!("{}", slice);  // 输出: 你好
}
```

#### 5. **总结**

Rust 提供了 `String` 和 `&str` 两种字符串类型，分别用于动态创建和修改字符串，以及对字符串的只读访问。通过这两种类型，Rust 能够高效地处理和操作字符串，同时确保内存安全。常用的字符串操作包括拼接、获取长度和遍历字符等，Rust 的字符串处理与 UTF-8 编码兼容，使其能够轻松处理多语言文本。
