# module.modulemap



{% hint style="info" %}
注意：使用pod管理不用写这个文件，

在podfile文件中声明为use\_modular\_headers! 就可以了。
{% endhint %}

在 `module.modulemap` 文件中，以下内容的意思是：

```modulemap
module MyLibrary {
    umbrella header "MyLibrary.h"
    export *
    module * { export * }
}
```

#### 各部分的解释

1. **`module MyLibrary`**:
   * 这行定义了一个名为 `MyLibrary` 的模块。模块是一个代码封装单元，允许你将多个相关的头文件和实现文件组织在一起。
2. **`umbrella header "MyLibrary.h"`**:
   * `umbrella header` 指定了一个主头文件（在这里是 `MyLibrary.h`），这个文件通常包含模块中所有其他头文件的导入。它为模块提供了一个统一的接口，其他代码可以通过包含这个头文件来访问模块的所有公共内容。
3. **`export *`**:
   * 这行指示编译器导出当前模块（`MyLibrary`）中的所有符号（例如，类、函数、变量等）。这意味着任何导入这个模块的代码都可以访问这些符号。
4. **`module * { export * }`**:
   * 这行定义了一个通配符模块（`*`），这意味着它适用于所有子模块。`export *` 的作用是导出这个通配符模块中所有符号。通常情况下，这种用法用于管理复杂的模块结构，确保子模块的所有符号都可以被访问。

#### 整体含义

整体来说，这段代码的作用是定义一个名为 `MyLibrary` 的模块，该模块的公共接口通过 `MyLibrary.h` 提供。模块中的所有符号都被导出，并且如果有子模块，它们的所有符号也会被导出。这使得用户能够通过简单的导入语句（`@import MyLibrary;`）来访问 `MyLibrary` 中的所有公共 API，而不需要单独导入每一个子模块的头文件。

#### 使用场景

这种模块化结构特别适用于较大或复杂的库，可以帮助开发者更好地管理代码的可见性和组织性，同时简化了用户的导入过程。
