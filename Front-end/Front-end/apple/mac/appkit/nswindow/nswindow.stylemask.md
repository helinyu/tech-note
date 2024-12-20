# NSWindow.StyleMask

以下是 `NSWindow.StyleMask` 中各个选项的详细说明及其作用：

#### 1. **`borderless`**

* **作用**: 创建一个没有边框的窗口，通常用于需要完全自定义外观的场景。此选项适用于自定义绘图和动画。
* **用途**: 适合创建特定的用户界面效果，如全屏应用或工具窗口。

#### 2. **`titled`**

* **作用**: 窗口具有标题栏。通常用于普通的窗口，以显示窗口的标题和控制按钮（关闭、最小化、放大）。
* **用途**: 大多数应用程序的标准窗口都使用此样式。

#### 3. **`closable`**

* **作用**: 窗口可以关闭，通常会显示关闭按钮。
* **用途**: 用于需要关闭功能的窗口，尤其是对话框和主窗口。

#### 4. **`miniaturizable`**

* **作用**: 窗口可以最小化，通常会显示最小化按钮。
* **用途**: 适用于需要经常切换窗口的应用程序，以便用户可以将其最小化到 Dock。

#### 5. **`resizable`**

* **作用**: 窗口可以调整大小。
* **用途**: 提供用户灵活性，适用于需要根据内容大小调整窗口的应用。

#### 6. **`texturedBackground`** (已弃用)

* **作用**: 窗口具有纹理背景样式，允许使用图像或纹理作为背景。
* **用途**: 在 macOS 11.0 之前用于创建视觉上吸引人的窗口样式，现已不推荐使用。

#### 7. **`unifiedTitleAndToolbar`**

* **作用**: 窗口的标题栏和工具栏合并为一个统一的标题栏，提供更整洁的外观。
* **用途**: 在需要节省垂直空间的应用中非常有用，适合现代 macOS 应用。

#### 8. **`fullScreen`** (macOS 10.7 及更高版本)

* **作用**: 窗口可以进入全屏模式，遮挡整个屏幕。
* **用途**: 适用于视频播放器、游戏或任何需要全屏显示的应用。

#### 9. **`fullSizeContentView`** (macOS 10.10 及更高版本)

* **作用**: 窗口的内容视图扩展到窗口的整个可用区域，标题栏不占用空间。
* **用途**: 适用于需要更大内容区域的应用，如绘图或文档编辑器。

#### 10. **`utilityWindow`**

* **作用**: 窗口适合用作辅助窗口，通常有更小的标题栏。
* **用途**: 常用于工具或面板窗口，提供额外功能而不干扰主窗口。

#### 11. **`docModalWindow`**

* **作用**: 文档模态窗口，通常与特定文档交互，阻止与其他窗口的交互。
* **用途**: 在需要用户完成某项任务后才能返回主窗口的场景中使用，如编辑文档。

#### 12. **`nonactivatingPanel`**

* **作用**: 窗口不会成为关键窗口，但仍会显示在其他窗口之上。
* **用途**: 用于提供信息或控制元素，而不强制用户与之交互。

#### 13. **`hudWindow`** (macOS 10.6 及更高版本)

* **作用**: 窗口的样式类似于 HUD（抬头显示），通常是半透明的，突出显示重要信息。
* **用途**: 适用于需要在背景上方显示信息的应用，如工具提示或状态信息。

#### 总结

使用 `NSWindow.StyleMask` 可以根据应用的需求灵活设置窗口的样式，提升用户体验。选择合适的样式掩码能够确保窗口在功能和视觉上的一致性。如果你有特定的用例或想法，欢迎继续交流！
