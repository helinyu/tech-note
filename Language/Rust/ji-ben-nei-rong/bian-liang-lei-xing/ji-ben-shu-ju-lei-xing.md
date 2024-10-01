# 基本数据类型

<mark style="color:red;">标量类型和复合类型。标量类型包括整数、浮点数、布尔值和字符；复合类型包括元组和数组</mark>



Rust 作为一门系统编程语言，提供了多种基本数据类型，以便处理不同类型的值。以下是 Rust 中的主要基本数据类型：

#### 1. **标量类型（Scalar Types）**

标量类型表示单个值，包括整数、浮点数、布尔值和字符。

**1.1. 整数类型**

整数类型用于存储没有小数部分的数字，可以是有符号或无符号的。Rust 提供了多种整数类型，不同的类型根据所能存储的范围和内存大小进行区分：

| 类型      | 大小      | 有符号/无符号 |
| ------- | ------- | ------- |
| `i8`    | 8-bit   | 有符号     |
| `i16`   | 16-bit  | 有符号     |
| `i32`   | 32-bit  | 有符号     |
| `i64`   | 64-bit  | 有符号     |
| `i128`  | 128-bit | 有符号     |
| `isize` | 系统架构相关  | 有符号     |
| `u8`    | 8-bit   | 无符号     |
| `u16`   | 16-bit  | 无符号     |
| `u32`   | 32-bit  | 无符号     |
| `u64`   | 64-bit  | 无符号     |
| `u128`  | 128-bit | 无符号     |
| `usize` | 系统架构相关  | 无符号     |

* **有符号整数（`i` 系列）**：可以存储正数、负数和零。
* **无符号整数（`u` 系列）**：只能存储正数和零。
* **`isize` 和 `usize`**：它们的大小取决于目标平台。例如，在 64 位架构上，`isize` 和 `usize` 都是 64 位的。

**示例：**

```rust
fn main() {
    let x: i32 = -42;  // 有符号整数
    let y: u32 = 42;   // 无符号整数
    println!("x = {}, y = {}", x, y);
}
```

**1.2. 浮点类型**

Rust 提供两种浮点类型，分别表示单精度和双精度浮点数：

| 类型    | 大小     | 精度  |
| ----- | ------ | --- |
| `f32` | 32-bit | 单精度 |
| `f64` | 64-bit | 双精度 |

* **默认类型**：Rust 中浮点类型的默认类型是 `f64`，因为它在现代 CPU 上的速度和 `f32` 相同，但精度更高。

**示例：**

```rust
fn main() {
    let x: f64 = 3.14;  // 双精度浮点数
    let y: f32 = 2.5;   // 单精度浮点数
    println!("x = {}, y = {}", x, y);
}
```

**1.3. 布尔类型**

Rust 中的布尔类型是 `bool`，它有两个可能的值：`true` 和 `false`。

**示例：**

```rust
fn main() {
    let is_true: bool = true;
    let is_false = false;  // 类型推断
    println!("is_true = {}, is_false = {}", is_true, is_false);
}
```

**1.4. 字符类型**

Rust 中的字符类型是 `char`，用于表示单个 Unicode 字符。Rust 的 `char` 类型占用 4 个字节，能够表示 Unicode 标准中的所有字符。

**示例：**

```rust
fn main() {
    let c: char = 'A';
    let heart_emoji: char = '❤️';
    println!("c = {}, heart_emoji = {}", c, heart_emoji);
}
```

#### 2. **复合类型（Compound Types）**

复合类型可以将多个值组合在一起，Rust 提供了两种主要的复合类型：元组和数组。

**2.1. 元组（Tuple）**

元组可以将多个类型不同的值组合在一起，长度是固定的。一旦声明，元组中的元素的数量和类型就不能改变。

**示例：**

```rust
fn main() {
    let tup: (i32, f64, char) = (500, 6.4, 'a');
    let (x, y, z) = tup;  // 解构元组
    println!("x = {}, y = {}, z = {}", x, y, z);

    // 通过索引访问元组
    let first_element = tup.0;
    println!("第一个元素是: {}", first_element);
}
```

**2.2. 数组（Array）**

数组存储固定长度的相同类型的元素。Rust 中的数组类型 `[T; N]` 表示包含 `N` 个元素的数组，其中每个元素的类型为 `T`。

**示例：**

```rust
fn main() {
    let arr: [i32; 5] = [1, 2, 3, 4, 5];  // 长度为 5 的整型数组
    let same_values = [3; 5];  // 长度为 5，所有元素都是 3

    println!("arr[0] = {}", arr[0]);  // 通过索引访问
    println!("same_values[1] = {}", same_values[1]);
}
```

#### 3. **类型推断与默认类型**

Rust 可以自动推断变量的类型，尤其是标量类型。比如，在没有明确指定类型的情况下，整数类型会默认为 `i32`，浮点数类型会默认为 `f64`。

**示例：**

```rust
fn main() {
    let x = 42;  // 默认为 i32
    let y = 3.14;  // 默认为 f64
    println!("x = {}, y = {}", x, y);
}
```

#### 4. **数值操作**

Rust 支持标准的数值操作符，如加法、减法、乘法、除法和取余。

**示例：**

```rust
fn main() {
    let sum = 5 + 10;
    let difference = 95.5 - 4.3;
    let product = 4 * 30;
    let quotient = 56.7 / 32.2;
    let remainder = 43 % 5;
    println!("sum = {}, difference = {}, product = {}, quotient = {}, remainder = {}",
             sum, difference, product, quotient, remainder);
}
```

#### 5. **总结**

Rust 的基本数据类型分为标量类型和复合类型。标量类型包括整数、浮点数、布尔值和字符；复合类型包括元组和数组。Rust 的类型系统严谨，避免了类型错误，提高了编译时的安全性。通过类型推断机制，Rust 也能在大多数情况下自动推断变量的类型，从而减少了手动指定类型的繁琐。
