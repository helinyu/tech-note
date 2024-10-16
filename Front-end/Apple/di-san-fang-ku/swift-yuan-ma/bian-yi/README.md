# 编译

编译和调试 Swift 源码可以分为编译 Swift 语言本身和编译使用 Swift 写的应用程序。以下是两者的具体步骤：

#### 一、编译 Swift 语言源码

编译 Swift 源码主要依赖于 CMake 和 Ninja 等工具。

**1. 环境准备**

* 确保已安装 **Git**、**CMake**、**Ninja**、**Python 3**。
* macOS 系统还需 **Xcode**。
* Linux 系统需安装一些编译依赖库，如 `libicu-dev`。

**2. 下载源码**

```bash
git clone https://github.com/apple/swift.git swift-source
cd swift-source
./utils/update-checkout --clone //  拉取 Swift 以及其依赖的项目（如 LLVM、Clang 和 lldb）
```

**3. 配置编译参数**

使用 `build-script` 脚本来编译 Swift，`build-script` 提供了很多编译选项。示例如下：

```bash
./utils/build-script -r //编译 Release 版本
./utils/build-script -d //编译 Debug  版本
```

这里的 `-r` 表示。如果需要 信息可以改为 `-d`。

**4. 编译**

编译市场取决于你的计算机性能。

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**5. 调试**

编译完成后，可以使用 LLDB（LLVM 提供的调试工具）来调试 Swift 的编译器源码：

```bash
lldb ./path/to/swift
```

你可以设置断点，观察各个模块的状态，查看 Swift 编译器的执行流程。

#### 二、编译和调试 Swift 应用程序

**1. 使用 Swift 命令行工具编译**

如果是简单的 Swift 项目，可以直接使用 `swiftc` 命令编译 Swift 源文件：

```bash
swiftc main.swift -o main
./main
```

**2. 使用 Xcode 编译和调试**

在 Xcode 中打开 Swift 项目后，可以通过以下步骤编译和调试：

* 选择目标设备或模拟器。
* 点击顶部工具栏的“运行”按钮进行编译并运行。
* 可以在左侧代码行号区域点击添加断点，调试时会自动停留在断点处。

在调试过程中，可以使用 Xcode 提供的 LLDB 调试工具，<mark style="color:purple;">查看变量、调用栈、内存等状态</mark>。

**3. 命令行调试**

在项目的根目录下，使用 `swift build` 命令可以编译 Swift 项目：

```bash
swift build -c debug
```

编译完成后，可以使用 LLDB 调试生成的可执行文件：

```bash
lldb .build/debug/YourExecutableName
```

使用这种方式可以模拟在 Xcode 中的调试体验，但适合用在 CI/CD 或远程调试中。
