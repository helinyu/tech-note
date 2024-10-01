# 模块/包

在 Rust 中，代码的组织方式主要通过模块、包和文件结构来实现，确保代码的可读性、可维护性和重用性。以下是 Rust 中代码组织的几个关键概念：

#### 1. **模块（Modules）**

模块是 Rust 中的基本组织单位，用于封装功能和相关代码。通过模块，可以控制访问权限和名称空间。

* **定义模块**：使用 `mod` 关键字定义模块。

```rust
mod my_module {
    pub fn my_function() {
        println!("Hello from my_module!");
    }
}
```

* **使用模块**：通过 `use` 关键字引入模块。

```rust
use my_module::my_function;

fn main() {
    my_function();
}
```

#### 2. **包（Packages）**

包是一个或多个模块的集合，可以编译成一个库或可执行文件。每个包都有一个 `Cargo.toml` 文件，定义包的元数据和依赖关系。

* **创建包**：使用 Cargo 创建新项目。

```bash
cargo new my_project
```

#### 3. **文件结构**

Rust 推荐使用特定的文件结构来组织模块和文件。每个模块通常在一个单独的文件中，模块目录可以用 `mod.rs` 文件表示。

* **单一文件模块**：将模块定义在同一个文件中。

```rust
// src/main.rs
mod my_module {
    pub fn my_function() { }
}

// src/main.rs
fn main() {
    my_module::my_function();
}
```

* **多文件模块**：将模块分散在多个文件中。

```rust
// src/my_module.rs
pub fn my_function() { }

// src/main.rs
mod my_module;

fn main() {
    my_module::my_function();
}
```

#### 4. **库与可执行文件**

Rust 项目可以是库或可执行文件。库使用 `lib.rs` 文件定义，可执行文件使用 `main.rs` 文件定义。

#### 5. **依赖管理**

使用 Cargo 管理依赖，可以在 `Cargo.toml` 文件中指定依赖项，Cargo 会自动处理版本和下载。

#### 6. **总结**

Rust 的代码组织通过模块、包和文件结构提供了灵活性和清晰度。模块化设计使得代码的封装、复用和维护变得简单，而 Cargo 提供了强大的依赖管理和构建系统，促进了 Rust 生态的繁荣。
