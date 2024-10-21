# 可设置的所有内容

以下是 `__attribute__` 可以设置的属性的详细列表，涵盖了常见及较少见的所有选项，以表格形式呈现：

| **属性名称**             | **作用**                                                   | **示例**                                                                  |
| -------------------- | -------------------------------------------------------- | ----------------------------------------------------------------------- |
| `aligned`            | 指定数据对齐方式                                                 | `int x __attribute__((aligned(16)));`                                   |
| `always_inline`      | 强制内联函数                                                   | `inline void func() __attribute__((always_inline));`                    |
| `cleanup`            | 在变量作用域结束时调用指定清理函数                                        | `int my_var __attribute__((cleanup(clean_func)));`                      |
| `cold`               | 表示函数不常调用，降低优化程度                                          | `void rarely_used() __attribute__((cold));`                             |
| `constructor`        | 指定函数在 `main` 之前执行，通常用于初始化                                | `void init() __attribute__((constructor));`                             |
| `deprecated`         | 标记函数或变量为“已废弃”，使用时产生警告                                    | `void old_func() __attribute__((deprecated));`                          |
| `destructor`         | 指定函数在 `main` 之后执行，通常用于清理                                 | `void cleanup() __attribute__((destructor));`                           |
| `error`              | 使用被标记的函数时会强制报错                                           | `void forbidden() __attribute__((error("Not allowed")));`               |
| `fallthrough`        | 防止编译器对 `switch` 语句的隐式穿透产生警告                              | `case 1: __attribute__((fallthrough));`                                 |
| `flatten`            | 优化函数调用路径中的内联                                             | `void func() __attribute__((flatten));`                                 |
| `format`             | 格式化检查，确保格式字符串和参数一致                                       | `void log(const char *fmt, ...) __attribute__((format(printf, 1, 2)));` |
| `format_arg`         | 指定参数作为格式化参数使用，类似 `printf`                                | `char *str_fmt(const char *fmt) __attribute__((format_arg(1)));`        |
| `gnu_inline`         | 使用 GNU 风格内联                                              | `inline void func() __attribute__((gnu_inline));`                       |
| `hot`                | 表示函数被频繁调用，编译器会更积极优化                                      | `void frequently_used() __attribute__((hot));`                          |
| `ifunc`              | 指定函数的间接实现                                                | `int func() __attribute__((ifunc("resolve_func")));`                    |
| `malloc`             | 函数类似 `malloc`，返回独立内存块                                    | `void* allocate(size_t size) __attribute__((malloc));`                  |
| `nonnull`            | 指定参数不能为空指针，若为空则警告                                        | `void func(int *ptr) __attribute__((nonnull));`                         |
| `noinline`           | 强制函数不内联                                                  | `void func() __attribute__((noinline));`                                |
| `noreturn`           | 指定函数无返回（如无限循环或异常终止）                                      | `void fatal() __attribute__((noreturn));`                               |
| `packed`             | 紧凑布局结构体，移除内存填充                                           | `struct __attribute__((packed)) MyStruct { int a; char b; };`           |
| `pure`               | 表示函数无副作用                                                 | `int square(int x) __attribute__((pure));`                              |
| `returns_nonnull`    | 指定函数返回值不为空指针，避免空指针检查                                     | `int* get_ptr() __attribute__((returns_nonnull));`                      |
| `section`            | 将变量或函数放入特定的内存段                                           | `int critical_data __attribute__((section(".mysection")));`             |
| `sentinel`           | 确保可变参数列表最后一个参数为空（例如 `NULL`）                              | `void func(int, ...) __attribute__((sentinel));`                        |
| `unused`             | 防止未使用的变量产生警告                                             | `int var __attribute__((unused));`                                      |
| `used`               | 告知编译器不要优化掉未被显式引用的符号                                      | `void func() __attribute__((used));`                                    |
| `visibility`         | 控制符号的可见性（如 `default`, `hidden`, `internal`, `protected`） | `int var __attribute__((visibility("hidden")));`                        |
| `warn_unused_result` | 如果函数返回值未使用则发出警告                                          | `int calculate() __attribute__((warn_unused_result));`                  |
| `weak`               | 将符号声明为弱符号，允许强符号覆盖                                        | `void my_func() __attribute__((weak));`                                 |
| `alias`              | 为符号提供别名                                                  | `void func() __attribute__((alias("other_func")));`                     |
| `nothrow`            | 声明函数不会抛出异常                                               | `void func() __attribute__((nothrow));`                                 |
| `assume_aligned`     | 提示编译器特定指针具有对齐要求，便于优化                                     | `void *aligned_ptr __attribute__((assume_aligned(16)));`                |
| `cleanup`            | 在变量超出作用域时调用指定的清理函数                                       | `int my_var __attribute__((cleanup(clean_func)));`                      |
| `transparent_union`  | 声明一个透明联合体，使联合体的成员可以直接访问                                  | `union __attribute__((transparent_union)) MyUnion { int i; float f; };` |
| `leaf`               | 表示函数为叶函数（不调用其他函数），可优化调用                                  | `void leaf_func() __attribute__((leaf));`                               |
| `vector_size`        | 指定向量的大小，便于 SIMD 优化                                       | `int vec __attribute__((vector_size(16)));`                             |

这些 `__attribute__` 提供了控制函数、变量、数据结构和编译器行为的灵活性。
