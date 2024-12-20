# \_\_attribute\_\_((visibility()))

`__attribute__((visibility("default")))` 是 GCC 和 Clang 提供的属性，用于控制符号的可见性，也就是<mark style="color:red;">**符号在编译后的二进制文件中是否对其他模块可见**</mark>。

#### 详细解释

* **`visibility("default")`**: 这是最常见的可见性选项，表示符号（如函数或变量）是公共的，可以被其他动态链接库或可执行文件引用和使用。它等价于 Windows 中的 `__declspec(dllexport)`。

#### 可见性选项

`visibility` 属性有几个选项，用于控制符号在编译后的二进制文件中的暴露程度：

* **`default`**：符号对外可见，可以在其他模块中被引用。
* **`hidden`**：符号仅在当前模块内可见，其他模块无法访问。可以减少命名冲突，提升安全性和优化性。
* **`internal`**：符号仅在当前文件内可见，类似 `static` 的作用。
* **`protected`**：符号对当前模块及继承模块可见。

#### 应用场景

在构建动态链接库时，设置符号可见性有助于控制接口和优化库的性能。例如，公共 API 可以使用 `default`，而内部实现可以使用 `hidden`，以确保只有必要的符号对外可见。
