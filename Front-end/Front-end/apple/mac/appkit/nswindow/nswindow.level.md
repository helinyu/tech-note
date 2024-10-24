# NSWindow.Level

在 macOS 开发中，`NSWindow.Level` 是用来定义窗口的层次（z-index）属性的。不同的层次会影响窗口的显示顺序以及它与其他窗口的交互方式。`NSWindow.Level` 是 `Int` 类型的枚举，值越大，窗口显示的层级越高。

一些常见的 `NSWindow.Level` 包括：

1. **`NSWindow.Level.normal`**
   * 普通窗口层级，应用程序的主窗口默认是这个层级。
2. **`NSWindow.Level.floating`**
   * 浮动层次，通常用于工具窗口。即使其他窗口获得焦点，浮动窗口仍保持在前。
3. **`NSWindow.Level.modalPanel`**
   * 模态对话框层次，模态窗口通常会在用户处理它之前阻止与其他窗口的交互。
4. **`NSWindow.Level.mainMenu`**
   * 用于菜单栏的窗口层次。
5. **`NSWindow.Level.statusBar`**
   * 用于状态栏窗口的层次。
6. **`NSWindow.Level.popUpMenu`**
   * 用于弹出菜单的窗口层次。
7. **`NSWindow.Level.screenSaver`**
   * 用于屏幕保护程序的窗口层次，是最高的层次，通常会遮盖所有其他窗口。

你可以通过以下方式设置窗口的层次：

```objective-c
[window setLevel:NSWindowLevelFloating];
```

