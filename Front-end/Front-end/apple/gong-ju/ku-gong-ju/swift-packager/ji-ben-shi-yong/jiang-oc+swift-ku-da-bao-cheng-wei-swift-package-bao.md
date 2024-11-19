# 将(OC+Swift)库打包成为swift package包

在 `Swift Package Manager` 的 `Package.swift` 文件中，可以通过 `path` 属性为每个目标（target）设置源码路径。下面是 Swift 和 Objective-C 源码路径配置的具体方法：

***

#### 示例目录结构

假设项目目录结构如下：

```
.
├── Package.swift
├── Sources
│   ├── SwiftCode         // Swift 源码目录
│   │   ├── SwiftFile1.swift
│   │   └── SwiftFile2.swift
│   ├── ObjectiveCCode    // Objective-C 源码目录
│       ├── ObjCFile1.m
│       ├── ObjCFile2.m
│       └── ObjCHeader.h
```

***

#### `Package.swift` 配置

将 Swift 和 Objective-C 分别设置为不同的目标。

**完整的 `Package.swift` 示例**

```swift
// swift-tools-version:5.5
import PackageDescription

let package = Package(
    name: "MixedLanguagePackage",
    platforms: [
        .iOS(.v13) // 根据项目需求设置支持的平台和版本
    ],
    products: [
        // 定义最终生成的库或可执行文件
        .library(
            name: "MixedLanguagePackage",
            targets: ["SwiftTarget"]
        )
    ],
    dependencies: [
        // 在这里添加外部依赖（如果需要）
    ],
    targets: [
        // Swift 目标
        .target(
            name: "SwiftTarget",
            dependencies: ["ObjectiveCTarget"], // 依赖 Objective-C 目标
            path: "Sources/SwiftCode"          // Swift 源码目录路径
        ),
        // Objective-C 目标
        .target(
            name: "ObjectiveCTarget",
            path: "Sources/ObjectiveCCode",    // Objective-C 源码目录路径
            publicHeadersPath: "."             // 指定头文件所在目录
        )
    ]
)
```

***

#### 配置说明

1. **`path` 参数**：
   * `path: "Sources/SwiftCode"`：指定 Swift 源码所在的目录。
   * `path: "Sources/ObjectiveCCode"`：指定 Objective-C 源码所在的目录。
2. **`publicHeadersPath` 参数**：
   * 对于 Objective-C 目标，必须指定头文件的公开路径。
   * `publicHeadersPath: "."` 表示头文件在指定目录下的根目录。
3. **依赖关系**：
   * 在 Swift 目标的 `dependencies` 中声明对 Objective-C 目标的依赖。
   * 这样，Swift 可以调用 Objective-C 的代码。

***

#### 头文件管理

Objective-C 的 `.m` 文件和 `.h` 文件应该放在 `Sources/ObjectiveCCode` 目录下。

1. 确保头文件（`.h`）包含在 `publicHeadersPath` 指定的路径中。
2. Swift 文件中调用 Objective-C 时，使用 `@_implementationOnly import ObjectiveCTarget`，或者通过桥接头文件引用。

***

#### 编译测试

1. 运行 `swift build` 检查是否成功。
2. 如果需要在 Xcode 中调试，可以通过 `swift package generate-xcodeproj` 生成 Xcode 项目文件。

***

在 `Package.swift` 文件中，为 Swift 和 Objective-C 目标添加依赖关系非常重要。以下是详细的配置步骤以及如何在 Swift 目标中依赖 Objective-C 目标的完整示例。

***

#### 示例目录结构

假设你的项目目录结构如下：

```
.
├── Package.swift
├── Sources
│   ├── SwiftCode         // Swift 源码目录
│   │   ├── SwiftFile1.swift
│   │   └── SwiftFile2.swift
│   ├── ObjectiveCCode    // Objective-C 源码目录
│       ├── ObjCFile1.m
│       ├── ObjCFile2.m
│       └── ObjCHeader.h
```

***

#### 完整的 `Package.swift` 示例

```swift
// swift-tools-version:5.5
import PackageDescription

let package = Package(
    name: "MixedLanguagePackage",
    platforms: [
        .iOS(.v13) // 根据需要设置支持的平台和最低版本
    ],
    products: [
        // 定义最终生成的库
        .library(
            name: "MixedLanguagePackage",
            targets: ["SwiftTarget"] // 最终暴露的主目标
        )
    ],
    dependencies: [
        // 添加外部依赖（如果需要）
    ],
    targets: [
        // Objective-C 目标
        .target(
            name: "ObjectiveCTarget",
            path: "Sources/ObjectiveCCode",    // Objective-C 代码路径
            publicHeadersPath: "."             // 头文件目录（路径相对于 ObjectiveCCode）
        ),
        // Swift 目标
        .target(
            name: "SwiftTarget",
            dependencies: ["ObjectiveCTarget"], // 声明对 Objective-C 目标的依赖
            path: "Sources/SwiftCode"          // Swift 代码路径
        ),
        // 测试目标（可选）
        .testTarget(
            name: "SwiftTargetTests",
            dependencies: ["SwiftTarget"],     // 测试目标依赖 Swift 目标
            path: "Tests/SwiftTargetTests"     // 测试代码路径
        )
    ]
)
```

***

#### 配置详解

1. **`ObjectiveCTarget`**：
   * `name: "ObjectiveCTarget"`：定义 Objective-C 的目标名称。
   * `path: "Sources/ObjectiveCCode"`：指定 Objective-C 源码的路径。
   * `publicHeadersPath: "."`：指定公开头文件路径。
     * 例如，如果 `Sources/ObjectiveCCode` 中有 `ObjCHeader.h`，Swift 目标可以通过 `import ObjectiveCTarget` 使用其中的符号。
2. **`SwiftTarget`**：
   * `name: "SwiftTarget"`：定义 Swift 的目标名称。
   * `dependencies: ["ObjectiveCTarget"]`：声明对 Objective-C 目标的依赖。
   * `path: "Sources/SwiftCode"`：指定 Swift 源码的路径。
3. **`publicHeadersPath`**：
   * 对于 `ObjectiveCTarget`，这个路径的头文件会暴露给 Swift 使用。
   * 在 Swift 目标中可以直接通过 `#import <ObjectiveCTarget/ObjCHeader.h>` 或直接调用依赖的代码。
4. **测试目标**：
   * `testTarget` 是可选的，通常用于单元测试。
   * 测试目标依赖主目标（例如 `SwiftTarget`）。

***

#### Swift 和 Objective-C 的交互

**在 Swift 中调用 Objective-C 代码**

1.  在 `ObjectiveCTarget` 中的头文件：

    ```objc
    // ObjCHeader.h
    #import <Foundation/Foundation.h>

    @interface ObjCExample : NSObject
    - (void)sayHello;
    @end
    ```
2.  在 `ObjectiveCTarget` 的实现文件：

    ```objc
    // ObjCFile1.m
    #import "ObjCHeader.h"

    @implementation ObjCExample
    - (void)sayHello {
        NSLog(@"Hello from Objective-C!");
    }
    @end
    ```
3.  在 `SwiftTarget` 中调用：

    ```swift
    import ObjectiveCTarget

    let example = ObjCExample()
    example.sayHello()
    ```

***

#### 测试和验证

1.  **运行 SPM 编译**：

    ```bash
    swift build
    ```
2.  **运行测试**：

    ```bash
    swift test
    ```
3.  如果需要生成 Xcode 工程并调试：

    ```bash
    swift package generate-xcodeproj
    ```

这样，Swift 和 Objective-C 的依赖关系会被正确处理。任何问题可以随时向我反馈！



