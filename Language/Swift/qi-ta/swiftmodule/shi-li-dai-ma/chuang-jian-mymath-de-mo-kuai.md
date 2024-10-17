# 创建MyMath的模块

#### 1. 创建一个 Swift 模块

假设我们创建一个名为 `MyMath` 的模块，提供一些基本的数学功能。

**目录结构**

```
MyMath/
├── Package.swift
├── Sources/
│   └── MyMath/
│       ├── MyMath.swift
└── Tests/
    └── MyMathTests/
        └── MyMathTests.swift
```

#### 2. `Package.swift` 文件

这个文件定义了模块的信息和依赖关系。

```swift
// MyMath/Package.swift
// swift-tools-version: 6.0

import PackageDescription

let package = Package(
    name: "MyMath",
    products: [
        .library(
            name: "MyMath",
            targets: ["MyMath"]),
    ],
    targets: [
        .target(
            name: "MyMath",
            dependencies: []),
        .testTarget(
            name: "MyMathTests",
            dependencies: ["MyMath"]),
    ]
)
```

#### 3. 模块的实现

在 `MyMath.swift` 文件中实现一些数学函数。

```swift
// MyMath/Sources/MyMath/MyMath.swift

public struct MyMath {
    public static func add(_ a: Int, _ b: Int) -> Int {
        return a + b
    }
    
    public static func subtract(_ a: Int, _ b: Int) -> Int {
        return a - b
    }
    
    public static func multiply(_ a: Int, _ b: Int) -> Int {
        return a * b
    }
    
    public static func divide(_ a: Int, _ b: Int) -> Int? {
        guard b != 0 else { return nil }
        return a / b
    }
}
```

#### 4. 单元测试

在 `MyMathTests.swift` 文件中编写单元测试，以验证我们的模块。

```swift
// MyMath/Tests/MyMathTests/MyMathTests.swift

import XCTest
@testable import MyMath

final class MyMathTests: XCTestCase {
    func testAdd() {
        XCTAssertEqual(MyMath.add(2, 3), 5)
    }
    
    func testSubtract() {
        XCTAssertEqual(MyMath.subtract(5, 2), 3)
    }
    
    func testMultiply() {
        XCTAssertEqual(MyMath.multiply(4, 5), 20)
    }
    
    func testDivide() {
        XCTAssertEqual(MyMath.divide(10, 2), 5)
        XCTAssertNil(MyMath.divide(10, 0))
    }
}
```

#### 5. 编译和测试模块

在项目的根目录下，打开终端并运行以下命令以编译和测试模块：

```bash
# 编译模块
swift build

# 运行测试
swift test
```

#### 6. 使用模块

可以在其他项目中导入并使用 `MyMath` 模块。假设你创建了一个新的 Swift 项目，以下是如何使用 `MyMath` 模块的示例代码：

```swift
// ExampleApp/main.swift

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

#### 7. 运行示例应用程序

如果你将这个示例应用程序放在一个新项目中，确保在 `Package.swift` 中添加 `MyMath` 模块作为依赖。然后运行项目即可看到输出。

通过以上步骤，你已经创建了一个完整的 Swift 模块并在其他项目中使用了它！如果有任何疑问或需要进一步的帮助，请告诉我。
