# 1、创建xcframework库

以下是使用 Swift 创建一个 XCFramework 的完整步骤和代码示例，包括如何生成多平台支持的框架并将其打包成 XCFramework。

***

#### 1. **创建 Swift Framework**

1. 打开 Xcode，选择 **File > New > Project**。
2. 选择 **Framework & Library > Framework**。
3. 设置名称为 `MyFramework`，选择语言为 **Swift**。
4. 创建项目并保存。

***

#### 2. **添加代码到框架**

在 `MyFramework` 项目的主文件中实现一个简单的功能。

**MyFramework.swift**

```swift
import Foundation

public class MyFramework {
    public static func sayHello() {
        print("Hello from MyFramework!")
    }
}
```

确保类和方法使用了 `public` 访问级别，这样外部项目才能调用。

***

#### 3. **设置支持的平台**

1. 点击项目文件（左侧导航栏顶端的项目名称）。
2. 在 **"Targets" > MyFramework > General > Framework Info** 中，勾选需要支持的平台（iOS、macOS、watchOS 或 tvOS）。
3. 在 **"Build Settings"** 中，确保：
   * **Build Active Architecture Only** 设置为 `No`。
   * 确保架构包含设备（`arm64`）和模拟器（`x86_64, arm64`）。

***

#### 4. **生成多平台框架**

需要分别为 **iOS 设备** 和 **iOS 模拟器** 构建框架。

**为 iOS 设备生成 `.framework`**

运行以下命令：

```bash
xcodebuild archive \
  -scheme MyFramework \
  -destination "generic/platform=iOS" \
  -archivePath ./build/ios_devices.xcarchive \
  SKIP_INSTALL=NO \
  BUILD_LIBRARIES_FOR_DISTRIBUTION=YES
```

**为 iOS 模拟器生成 `.framework`**

运行以下命令：

```bash
xcodebuild archive \
  -scheme MyFramework \
  -destination "generic/platform=iOS Simulator" \
  -archivePath ./build/ios_simulator.xcarchive \
  SKIP_INSTALL=NO \
  BUILD_LIBRARIES_FOR_DISTRIBUTION=YES
```

这两个命令将在 `./build/ios_devices.xcarchive` 和 `./build/ios_simulator.xcarchive` 目录下生成框架文件。

***

#### 5. **创建 XCFramework**

使用 `xcodebuild` 将设备和模拟器的框架打包成一个 XCFramework：

```bash
xcodebuild -create-xcframework \
  -framework ./build/ios_devices.xcarchive/Products/Library/Frameworks/MyFramework.framework \
  -framework ./build/ios_simulator.xcarchive/Products/Library/Frameworks/MyFramework.framework \
  -output ./build/MyFramework.xcframework
```

***

#### 6. **验证生成的 XCFramework**

确认生成的 `MyFramework.xcframework` 是否包含不同平台的支持文件，结构如下：

```
MyFramework.xcframework/
├── Info.plist
├── ios-arm64/
│   └── MyFramework.framework
├── ios-arm64_x86_64-simulator/
│   └── MyFramework.framework
```

***

#### 7. **在项目中使用 XCFramework**

1. 将生成的 `MyFramework.xcframework` 拖入你的主项目。
2. 确保 **"Build Phases > Link Binary with Libraries"** 包含 `MyFramework.xcframework`。
3. 在需要使用的文件中导入框架并调用其方法：

**示例代码：**

```swift
import MyFramework

MyFramework.sayHello()
```

***

#### 扩展支持其他平台

如果需要支持其他平台（如 macOS、tvOS、watchOS），可以重复以上步骤，为每个平台生成 `.framework` 文件，并将其添加到 `xcodebuild -create-xcframework` 命令中。例如：

```bash
xcodebuild -create-xcframework \
  -framework ./build/ios_devices.xcarchive/Products/Library/Frameworks/MyFramework.framework \
  -framework ./build/ios_simulator.xcarchive/Products/Library/Frameworks/MyFramework.framework \
  -framework ./build/macos.xcarchive/Products/Library/Frameworks/MyFramework.framework \
  -output ./build/MyFramework.xcframework
```

***

#### 总结

通过以上步骤，你可以使用 Swift 创建一个支持多平台的 XCFramework。XCFramework 是 Apple 现代化的框架打包方式，适合需要在多个设备（如 iPhone、iPad 和 macOS）上分发框架的场景。
