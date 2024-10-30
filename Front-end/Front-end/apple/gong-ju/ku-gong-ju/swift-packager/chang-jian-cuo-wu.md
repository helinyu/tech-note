# 常见错误

## 1、clang: error: no such file or directory:

clang: error: no such file or directory: '/Users/helinyu/Library/Developer/Xcode/DerivedData/TestSwiftExmaple-cglsdhrhidjznhbpycozaliyaams/Build/Products/Debug-iphonesimulator/PackageFrameworks/AlamofireDynamic.framework/AlamofireDynamic'

这个是因为项目里卖弄使用了动态库，所以我们要将静态库去掉。

删除灭有dynamic的这个静态库。



### 2、为什么导入就是两个库

在 Swift 项目中导入 SnapKit 时，如果你看到两个不同的依赖项 —— 一个是 `SnapKit`，另一个是 `SnapKit Dynamic`，这是由于它们的编译方式和链接方式的不同：

1. **SnapKit**：
   * 这是静态库（**static framework**）。
   * 当你导入静态库时，库的代码会在编译时直接链接到你的应用程序中，并成为应用的一部分。静态库的好处是性能更好，因为它不需要在运行时加载外部库，但应用体积可能会增加。
2. **SnapKit Dynamic**：
   * 这是动态库（**dynamic framework**）。
   * 动态库在运行时动态链接，不会直接嵌入到应用程序中，而是独立的库文件。这样可以减小应用的体积，因为多个应用可以共享同一个动态库，但运行时需要加载库，可能会有少许的性能开销。

**为什么会出现这两种？**

在某些项目中，开发者可能需要使用静态库以优化性能和减少动态链接的复杂性。对于需要动态链接的场景，比如希望库可以在运行时更新或在多个目标之间共享库，则会使用动态库。

一些依赖管理工具（如 Swift Package Manager 或 CocoaPods）在集成依赖时，会自动提供静态和动态版本的选择，取决于项目的设置。

**如何选择？**

* **静态库** (`SnapKit`)：如果你希望将库代码直接打包到应用中，并且不需要动态链接或插件化支持，可以选择静态版本。适合性能要求较高的应用。
* **动态库** (`SnapKit Dynamic`)：如果你需要动态加载库，或者库的版本可能需要在运行时进行更新，则选择动态版本。

通常，默认选择静态库即可，除非你的项目明确需要动态库。

