# 使用MyMath模块

在 Swift 中使用模块（如 `MyMath` 模块）的步骤如下。这些步骤将引导你如何在项目中导入和使用这个模块。

#### 1. 创建和设置 Swift 项目

如果你还没有创建一个 Swift 项目，可以使用 Swift Package Manager (SPM) 创建一个新项目。假设我们要创建一个名为 `ExampleApp` 的新项目：

```bash
mkdir ExampleApp
cd ExampleApp
swift package init --type executable
```

#### 2. 更新 `Package.swift`

在 `ExampleApp` 目录中，打开 `Package.swift` 文件，并将 `MyMath` 模块作为依赖项添加。确保先将 `MyMath` 模块的路径设置为相对路径，像这样：

```swift
// swift-tools-version: 6.0
import PackageDescription

let package = Package(
    name: "ExampleApp",
    dependencies: [
        .package(path: "../MyMath") // 指向 MyMath 模块的相对路径
    ],
    targets: [
        .target(
            name: "ExampleApp",
            dependencies: ["MyMath"]), // 这一句别漏掉
        .testTarget(
            name: "ExampleAppTests",
            dependencies: ["ExampleApp"]),
    ]
)
```

#### 3. 使用模块

在 `Sources/ExampleApp/main.swift` 文件中，导入 `MyMath` 模块并使用它。以下是示例代码：

```swift
// ExampleApp/Sources/ExampleApp/main.swift

import MyMath

let sum = MyMath.add(10, 20)
let difference = MyMath.subtract(30, 10)
let product = MyMath.multiply(5, 6)
let quotient = MyMath.divide(20, 4)

print("Sum: \(sum)")
print("Difference: \(difference)")
print("Product: \(product)")
print("Quotient: \(String(describing: quotient))")
```

#### 4. 运行应用程序

在 `ExampleApp` 项目的根目录下，打开终端并运行以下命令以编译和运行项目：

```bash
swift package update // 更新package的内容
swift build
swift run
```

#### 5. 预期输出

当你运行 `swift run` 时，应该看到如下输出：

```
Sum: 30
Difference: 20
Product: 30
Quotient: Optional(5)
```

#### 小结

* **创建新项目**: 使用 Swift Package Manager 创建一个新的可执行项目。
* **添加依赖项**: 在 `Package.swift` 中添加对 `MyMath` 模块的依赖。
* **导入并使用模块**: 在你的 Swift 文件中导入模块并调用其函数。
* **编译和运行**: 使用 `swift build` 和 `swift run` 来编译和运行项目。
