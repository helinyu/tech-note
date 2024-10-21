# 分类

`__attribute__` 提供了控制**函数、变量、数据结构、编译器行为**的多种功能，下面按作用对象分类列出常见的 `__attribute__` 用法：

#### 1. **函数相关的 `__attribute__`**

| **属性名称**             | **作用**                     | **示例**                                                                  |
| -------------------- | -------------------------- | ----------------------------------------------------------------------- |
| `always_inline`      | 强制内联函数                     | `inline void func() __attribute__((always_inline));`                    |
| `noinline`           | 强制函数不内联                    | `void func() __attribute__((noinline));`                                |
| `noreturn`           | 指定函数不返回值（如异常终止、死循环）        | `void fatal_error() __attribute__((noreturn));`                         |
| `pure`               | 表示函数无副作用，仅依赖参数输入           | `int get_value(int x) __attribute__((pure));`                           |
| `const`              | 表示函数无副作用且无外部依赖，仅依赖参数输入     | `int square(int x) __attribute__((const));`                             |
| `format`             | 格式化参数检查，确保格式字符串和参数一致       | `void log(const char *fmt, ...) __attribute__((format(printf, 1, 2)));` |
| `hot`                | 提示编译器函数使用频繁，优化指令生成         | `void fast_func() __attribute__((hot));`                                |
| `cold`               | 提示编译器函数使用不频繁，降低优化优先级       | `void slow_func() __attribute__((cold));`                               |
| `warn_unused_result` | 警告未使用函数的返回值                | `int compute() __attribute__((warn_unused_result));`                    |
| `leaf`               | 表示函数为叶函数（不调用其他函数），便于编译器优化  | `void leaf_func() __attribute__((leaf));`                               |
| `error`              | 强制在调用函数时产生编译错误             | `void forbidden() __attribute__((error("Not allowed")));`               |
| `constructor`        | 在 `main` 函数之前执行的函数，通常用于初始化 | `void init() __attribute__((constructor));`                             |
| `destructor`         | 在 `main` 退出后执行的函数，通常用于资源清理 | `void cleanup() __attribute__((destructor));`                           |

#### 2. **变量相关的 `__attribute__`**

| **属性名称**     | **作用**                                                   | **示例**                                              |
| ------------ | -------------------------------------------------------- | --------------------------------------------------- |
| `aligned`    | 指定变量对齐方式                                                 | `int x __attribute__((aligned(16)));`               |
| `unused`     | 防止编译器对未使用的变量产生警告                                         | `int var __attribute__((unused));`                  |
| `used`       | 保留未显式引用的符号，防止优化掉                                         | `int var __attribute__((used));`                    |
| `cleanup`    | 在变量超出作用域时调用清理函数                                          | `int var __attribute__((cleanup(cleanup_func)));`   |
| `deprecated` | 标记变量为已废弃，使用时产生警告                                         | `int old_var __attribute__((deprecated));`          |
| `visibility` | 设置符号的可见性（如 `default`, `hidden`, `internal`, `protected`） | `int var __attribute__((visibility("hidden")));`    |
| `section`    | 将变量放入指定的内存段                                              | `int data __attribute__((section(".my_section")));` |
| `weak`       | 声明弱符号，允许被其他模块中的同名强符号覆盖                                   | `int weak_var __attribute__((weak));`               |

#### 3. **数据结构（结构体/联合体）相关的 `__attribute__`**

| **属性名称**            | **作用**                  | **示例**                                                                  |
| ------------------- | ----------------------- | ----------------------------------------------------------------------- |
| `packed`            | 紧凑布局结构体，移除内存填充          | `struct __attribute__((packed)) MyStruct { int a; char b; };`           |
| `aligned`           | 设置结构体对齐方式               | `struct __attribute__((aligned(16))) AlignedStruct { int a; };`         |
| `transparent_union` | 透明联合体，允许直接访问成员          | `union __attribute__((transparent_union)) MyUnion { int i; float f; };` |
| `may_alias`         | 告知编译器允许该类型作为别名访问其他类型的数据 | `typedef int my_alias __attribute__((may_alias));`                      |
| `deprecated`        | 标记结构体为已废弃，使用时产生警告       | `struct OldStruct __attribute__((deprecated)) { int a; };`              |

#### 4. **编译器行为相关的 `__attribute__`**

| **属性名称**         | **作用**                              | **示例**                                                              |
| ---------------- | ----------------------------------- | ------------------------------------------------------------------- |
| `alias`          | 为符号提供别名                             | `void new_func() __attribute__((alias("old_func")));`               |
| `visibility`     | 控制符号的模块间可见性（例如 `default`, `hidden`） | `int var __attribute__((visibility("hidden")));`                    |
| `optimize`       | 为指定函数或代码块设置优化级别                     | `void func() __attribute__((optimize("O2")));`                      |
| `target`         | 指定函数的编译目标架构                         | `void func() __attribute__((target("sse2")));`                      |
| `flatten`        | 优化内联与函数调用，展开所有直接调用的函数               | `void func() __attribute__((flatten));`                             |
| `nothrow`        | 指定函数不抛出异常                           | `void safe_func() __attribute__((nothrow));`                        |
| `error`          | 使用符号时产生编译错误                         | `void restricted() __attribute__((error("Cannot use")));`           |
| `warning`        | 使用符号时产生编译警告                         | `void caution_func() __attribute__((warning("Use with caution")));` |
| `assume_aligned` | 提示编译器指针有对齐要求，便于生成优化代码               | `void *ptr __attribute__((assume_aligned(16)));`                    |
| `fallthrough`    | 防止 `switch` 语句的隐式穿透产生警告             | `case 1: __attribute__((fallthrough));`                             |
| `weakref`        | 为符号提供弱引用，允许同名强符号覆盖                  | `void func() __attribute__((weakref("other_func")));`               |

这些属性的分类帮助我们有针对性地使用 `__attribute__` 来优化函数、变量、数据结构的行为，并为编译器设置更多控制选项，提高代码的效率和安全性。
