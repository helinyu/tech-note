# 标准IO输出

在 Rust 中，标准输出主要通过 `std::io` 模块进行操作。以下是使用标准输出的一些基本内容和示例：

#### 1. **使用 `println!` 宏**

最常用的标准输出方式是 `println!` 宏，它用于打印带有换行的文本到控制台。

```rust
fn main() {
    println!("Hello, World!");
}
```

#### 2. **格式化输出**

`println!` 支持格式化输出，可以使用占位符来插入变量的值。

```rust
let name = "Alice";
let age = 30;
println!("{} is {} years old.", name, age);
```

#### 3. **使用 `print!` 宏**

`print!` 宏类似于 `println!`，但不会自动换行。

```rust
print!("This will be printed on the same line.");
```

#### 4. **使用 `std::io::stdout`**

对于更复杂的输出需求，可以直接使用 `std::io::stdout()`。

```rust
use std::io::{self, Write};

fn main() {
    let mut stdout = io::stdout();
    stdout.write_all(b"Hello, World!\n").unwrap();
}
```

#### 5. **缓冲输出**

使用 `BufWriter` 可以对输出进行缓冲，提升性能，尤其是在需要频繁写入的情况下。

```rust
use std::fs::File;
use std::io::{self, BufWriter};

fn main() -> io::Result<()> {
    let file = File::create("output.txt")?;
    let mut writer = BufWriter::new(file);
    writeln!(writer, "Hello, World!")?;
    Ok(())
}
```

#### 6. **总结**

Rust 的标准输出提供了简单且灵活的方式来打印信息。通过使用 `println!`、`print!` 以及直接操作 `std::io`，你可以轻松实现各种输出需求。使用缓冲输出可以提高性能，尤其在处理大量数据时。
