# 标准IO输入

在 Rust 中，标准输入主要通过 `std::io` 模块进行操作。以下是使用标准输入的一些基本内容和示例：

#### 1. **使用 `io::stdin()`**

最常用的读取标准输入的方法是通过 `io::stdin()`。

```rust
use std::io;

fn main() {
    let mut input = String::new();

    println!("请输入一些文本:");
    io::stdin()
        .read_line(&mut input)
        .expect("读取输入失败");

    println!("你输入的内容是: {}", input.trim());
}
```

#### 2. **处理输入**

`read_line` 方法会将输入读取到指定的 `String` 中，并在末尾添加换行符。通常使用 `trim()` 方法去除多余的空白字符。

#### 3. **读取多个输入**

可以使用循环读取多次输入。

```rust
use std::io;

fn main() {
    let mut input = String::new();

    loop {
        input.clear(); // 清空之前的输入
        println!("请输入一些文本 (输入 'exit' 退出):");
        io::stdin().read_line(&mut input).expect("读取输入失败");
        
        if input.trim() == "exit" {
            break;
        }

        println!("你输入的内容是: {}", input.trim());
    }
}
```

#### 4. **从标准输入读取数字**

如果要读取数字，可以使用 `parse` 方法进行转换。

```rust
use std::io;

fn main() {
    let mut input = String::new();

    println!("请输入一个数字:");
    io::stdin().read_line(&mut input).expect("读取输入失败");

    let number: i32 = input.trim().parse().expect("请输入有效数字");
    println!("你输入的数字是: {}", number);
}
```

#### 5. **使用 `std::io::BufRead`**

如果需要读取多个行或其他更复杂的输入，可以使用 `BufReader`。

```rust
use std::io::{self, BufRead};

fn main() {
    let stdin = io::stdin();
    let handle = stdin.lock();

    println!("请输入多行文本，输入空行结束:");

    for line in handle.lines() {
        let line = line.expect("读取行失败");
        if line.is_empty() {
            break;
        }
        println!("你输入的内容是: {}", line);
    }
}
```

#### 6. **错误处理**

处理输入时，确保检查和处理可能的错误，避免程序崩溃。

#### 7. **总结**

Rust 的标准输入通过 `std::io` 提供了简单有效的方式来读取用户输入。使用 `io::stdin()` 和 `read_line()` 方法，你可以轻松地获取用户输入并进行处理。
