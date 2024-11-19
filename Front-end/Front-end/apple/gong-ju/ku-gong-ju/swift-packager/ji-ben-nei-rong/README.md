# 基本内容

在 **Swift Package Manager (SPM)** 中，`Package.swift` 是用来定义包配置的文件，它通过声明式的 API 描述一个包的结构、依赖、目标等内容。以下是 `Package.swift` 文件中常见关键字及其概念的详细解释：

***

#### **关键字概览**

**1. `Package`**

* **概念**：定义整个 Swift 包的入口。
* **功能**：描述包的基本信息，包括名称、版本要求、依赖和目标。
*   **示例**：

    ```swift
    let package = Package(
        name: "MyPackage",
        platforms: [.iOS("14.0")],
        products: [
            .library(name: "MyLibrary", targets: ["MyTarget"])
        ],
        dependencies: [
            .package(url: "https://github.com/apple/example-package.git", from: "1.0.0")
        ],
        targets: [
            .target(name: "MyTarget", dependencies: []),
            .testTarget(name: "MyTargetTests", dependencies: ["MyTarget"])
        ]
    )
    ```

***

**2. `name`**

* **概念**：定义包的名称。
* **功能**：这是包的唯一标识，常用于项目管理工具或依赖解析。
* **注意**：名称应简洁且具有描述性，通常与存储库名称一致。
*   **示例**：

    ```swift
    name: "MyPackage"
    ```

***

**3. `platforms`**

* **概念**：指定包支持的平台及其最低版本。
* **功能**：限定包的可用范围，确保依赖包在特定平台上运行。
*   **示例**：

    ```swift
    platforms: [
        .iOS("13.0"),
        .macOS("10.15")
    ]
    ```
* **支持的平台**：
  * `.iOS`
  * `.macOS`
  * `.tvOS`
  * `.watchOS`

***

**4. `products`**

* **概念**：定义包的输出产品。
* **功能**：描述包构建后生成的库或可执行文件，供其他包或项目使用。
* **类型**：
  * `.library`：静态或动态库。
  * `.executable`：命令行工具或其他可执行文件。
*   **示例**：

    ```swift
    products: [
        .library(
            name: "MyLibrary",
            targets: ["MyTarget"]
        ),
        .executable(
            name: "MyTool",
            targets: ["MyExecutableTarget"]
        )
    ]
    ```

***

**5. `dependencies`**

* **概念**：定义包的依赖。
* **功能**：列出包依赖的其他 Swift 包，支持从远程 URL 或本地路径添加依赖。
*   **示例**：

    ```swift
    dependencies: [
        .package(url: "https://github.com/apple/example-package.git", from: "1.0.0")
    ]
    ```
* **版本规则**：
  * `.exact("1.0.0")`：指定精确版本。
  * `.upToNextMajor(from: "1.0.0")`：支持 1.0.x，但不支持 2.0。
  * `.upToNextMinor(from: "1.0.0")`：支持 1.0.x 和 1.1.x，但不支持 1.2 或更高。
  * `.branch("main")`：指定分支。
  * `.revision("commit-hash")`：指定特定提交。

***

**6. `targets`**

* **概念**：定义包的构建单元。
* **功能**：指定包的代码模块及其依赖。
* **类型**：
  * `.target`：生产代码模块。
  * `.testTarget`：测试模块。
*   **示例**：

    ```swift
    targets: [
        .target(
            name: "MyTarget",
            dependencies: []
        ),
        .testTarget(
            name: "MyTargetTests",
            dependencies: ["MyTarget"]
        )
    ]
    ```

***

**7. `dependencies` (在 targets 中)**

* **概念**：定义当前 target 的依赖。
* **功能**：指定一个 target 所依赖的其他 targets 或外部包。
*   **示例**：

    ```swift
    .target(
        name: "MyTarget",
        dependencies: [
            "AnotherTarget",
            .product(name: "SomeLibrary", package: "example-package")
        ]
    )
    ```

***

**8. `path`**

* **概念**：指定目标代码所在的文件路径。
* **功能**：用于指定自定义的源码目录，而不是默认的 `Sources/TargetName`。
*   **示例**：

    ```swift
    .target(
        name: "MyTarget",
        path: "CustomSources/MyTarget"
    )
    ```

***

**9. `exclude`**

* **概念**：排除某些文件或文件夹。
* **功能**：防止 SPM 将不相关的文件包含进构建中。
*   **示例**：

    ```swift
    .target(
        name: "MyTarget",
        exclude: ["Tests", "OldCode"]
    )
    ```

***

**10. `resources`**

* **概念**：指定资源文件（如图片、配置文件等）。
* **功能**：让资源文件与代码一起打包。
*   **示例**：

    ```swift
    .target(
        name: "MyTarget",
        resources: [
            .process("Assets"),
            .copy("StaticFiles/ReadMe.txt")
        ]
    )
    ```

***

**11. `publicHeadersPath`**

* **概念**：用于目标中包含 C/Objective-C 文件时，指定头文件路径。
* **功能**：暴露目标的公共头文件，以便其他目标或依赖包使用。
*   **示例**：

    ```swift
    .target(
        name: "MyCTarget",
        publicHeadersPath: "include"
    )
    ```

***

**12. `cSettings` / `cxxSettings` / `swiftSettings`**

* **概念**：为不同的编程语言设置编译选项。
* **功能**：提供编译器标志、宏定义或其他编译配置。
*   **示例**：

    ```swift
    .target(
        name: "MyTarget",
        cSettings: [
            .headerSearchPath("include"),
            .define("DEBUG", .when(configuration: .debug))
        ],
        swiftSettings: [
            .define("ENABLE_FEATURE")
        ]
    )
    ```

***

**13. `plugins`**

* **概念**：定义目标的插件依赖。
* **功能**：为构建阶段添加自定义任务或行为。
*   **示例**：

    ```swift
    .target(
        name: "MyTarget",
        plugins: [
            .plugin(name: "MyCustomPlugin")
        ]
    )
    ```

***

#### **总结**

`Package.swift` 的各个关键字让 Swift 包的定义更加灵活和模块化。通过合理使用这些关键字，你可以构建和管理复杂的 Swift 包生态，同时轻松维护代码的依赖和目标结构。
