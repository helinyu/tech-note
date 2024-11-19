# 示例

下面是一个**完整、全面的 `Package.swift` 文件**示例，涵盖了 Swift Package Manager 中常用的功能和关键字，展示了如何定义一个复杂的 Swift 包结构。

#### 完整示例

```swift
// swift-tools-version:5.9
import PackageDescription

let package = Package(
    name: "MyComprehensivePackage", // 包名称
    defaultLocalization: "en",      // 默认的本地化语言
    platforms: [                    // 指定支持的平台及最低版本
        .iOS("14.0"),
        .macOS("12.0"),
        .tvOS("15.0"),
        .watchOS("8.0")
    ],
    products: [                     // 定义包的输出产品
        .library(
            name: "CoreLibrary",
            targets: ["CoreTarget"]
        ),
        .library(
            name: "UILibrary",
            targets: ["UITarget"]
        ),
        .executable(
            name: "MyExecutable",
            targets: ["ExecutableTarget"]
        )
    ],
    dependencies: [                 // 定义包的外部依赖
        .package(
            url: "https://github.com/apple/swift-argument-parser.git",
            from: "1.2.0"
        ),
        .package(
            url: "https://github.com/Quick/Quick.git",
            .upToNextMajor(from: "4.0.0")
        ),
        .package(
            url: "https://github.com/Realm/realm-swift.git",
            .exact("10.39.0")
        )
    ],
    targets: [                      // 定义包的构建单元（targets）
        // 主库 Target
        .target(
            name: "CoreTarget",
            dependencies: [
                .product(name: "RealmSwift", package: "realm-swift")
            ],
            path: "Sources/Core",
            exclude: ["OldFiles"],
            resources: [
                .process("Resources/Config.json")
            ],
            swiftSettings: [
                .define("ENABLE_LOGGING"),
                .unsafeFlags(["-enable-library-evolution"], .when(configuration: .release))
            ]
        ),
        // UI 相关的 Target
        .target(
            name: "UITarget",
            dependencies: [
                "CoreTarget"
            ],
            path: "Sources/UI",
            resources: [
                .process("Assets.xcassets"),
                .copy("Static/License.txt")
            ]
        ),
        // 命令行工具 Target
        .executableTarget(
            name: "ExecutableTarget",
            dependencies: [
                "CoreTarget",
                .product(name: "ArgumentParser", package: "swift-argument-parser")
            ],
            path: "Sources/Executable"
        ),
        // 测试 Target
        .testTarget(
            name: "CoreTests",
            dependencies: [
                "CoreTarget",
                "Quick"
            ],
            path: "Tests/CoreTests",
            resources: [
                .process("TestResources/TestData.json")
            ]
        )
    ],
    swiftLanguageVersions: [        // 指定支持的 Swift 语言版本
        .v5
    ]
)
```

***

#### **功能详解**

1. **基本信息**：
   * **`name`**: 包名。
   * **`defaultLocalization`**: 指定包的默认语言。
   * **`platforms`**: 限制包可用的平台及最低版本。
2. **`products`**：
   * 包含多个库（`library`）和可执行文件（`executable`），用于定义外部可见的产品。
3. **`dependencies`**：
   * 定义了三个依赖：
     * `swift-argument-parser` 用于命令行工具。
     * `Quick` 用于测试框架。
     * `realm-swift` 作为数据库库。
4. **`targets`**：
   * **`CoreTarget`**:
     * 主核心模块，包含资源文件（`Config.json`）并支持 Swift 设置（`ENABLE_LOGGING`）。
   * **`UITarget`**:
     * UI 模块，依赖核心模块并包含图形资源（`Assets.xcassets`）。
   * **`ExecutableTarget`**:
     * 可执行文件模块，依赖于 `CoreTarget` 和 `swift-argument-parser`。
   * **`CoreTests`**:
     * 测试模块，依赖于 `Quick` 和 `CoreTarget`，包括测试数据资源。
5. **高级设置**：
   * **`swiftSettings`**: 用于定义 Swift 编译器的配置，例如启用特定功能标志。
   * **`resources`**: 支持 `.process` 和 `.copy` 两种方式处理资源。
   * **`swiftLanguageVersions`**: 指定支持的 Swift 语言版本。

***

#### **目录结构对应示例**

```plaintext
MyComprehensivePackage/
├── Package.swift
├── Sources/
│   ├── Core/
│   │   ├── Models.swift
│   │   ├── Utils.swift
│   │   ├── Resources/
│   │   │   └── Config.json
│   │   └── OldFiles/
│   └── UI/
│       ├── View.swift
│       ├── Assets.xcassets/
│       └── Static/
│           └── License.txt
│   └── Executable/
│       ├── main.swift
│       └── Command.swift
├── Tests/
│   └── CoreTests/
│       ├── CoreTests.swift
│       ├── TestResources/
│       │   └── TestData.json
```

***

#### **使用场景**

1. **模块化开发**：
   * 将核心逻辑和 UI 逻辑分离到不同的 targets，便于复用和测试。
2. **资源管理**：
   * 使用 `resources` 配置处理 JSON、图片等资源文件。
3. **测试驱动开发**：
   * 使用 `testTarget` 定义测试模块，依赖 `Quick` 测试框架。
4. **可扩展性**：
   * 添加第三方依赖（如 Realm 和 ArgumentParser），实现快速集成。

这个示例展示了一个复杂的、多模块的 Swift Package 项目，涵盖了大部分 SPM 的功能，适用于实际开发中的多种需求。
