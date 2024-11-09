# becomeKey vs makeKey

`becomeKey()` 和 `makeKey()` 在 iOS 和 macOS 开发中都与视图的“键视图”（key view）相关，通常出现在 `UIWindow` 或 `NSWindow` 的上下文中。尽管它们名字相似，实际上它们用于不同的目的，而且在平台上也有所区别。

#### 1. `becomeKey()`

`becomeKey()` 是 `UIWindow` 或 `NSWindow` 的方法，用于使窗口成为 **"键窗口"**，即获得焦点并能够接收事件（如触摸事件、鼠标点击等）。

* **平台**：主要在 macOS 上使用，也适用于 iOS 中的 `UIWindow` 类。
* **功能**：该方法会将当前的窗口或视图设为“键视图”并接收输入事件，通常用来处理用户交互。
* **返回值**：没有返回值，直接影响窗口的行为。

**使用场景：**

* 在 **macOS** 中，`becomeKey()` 使得一个窗口成为当前应用的主窗口，接受事件。
* 在 **iOS** 中，`UIWindow` 会根据 `becomeKey()` 自动接收事件。

**示例（macOS）：**

```objc
[myWindow becomeKeyWindow];
```

在 macOS 中，调用 `becomeKeyWindow` 会将 `myWindow` 设置为键窗口。

#### 2. `makeKey()`

`makeKey()` 是在 **macOS** 开发中较为常见的方法，特别是涉及到 **`NSWindow`**。它和 `becomeKey()` 的作用类似，都是将一个窗口设置为键窗口。但是在 API 上，这两个方法在不同版本的 macOS 和 iOS 中可能会有所不同，或许你会看到 `makeKeyAndOrderFront()` 这样的方法。

* **平台**：主要在 macOS 中使用，`makeKey()` 实际上是 `NSWindow` 的一个方法。
* **功能**：将窗口设为键窗口并且将窗口置于最前面。与 `becomeKey()` 相比，`makeKey()` 通常也会将窗口置于前面。

**使用场景：**

* 在 **macOS** 中，`makeKeyAndOrderFront()` 通常用于将窗口放到前面并让它成为键窗口。例如，在弹出窗口时，确保该窗口在用户的视野前端并接收焦点。

**示例（macOS）：**

```objc
[myWindow makeKeyAndOrderFront:nil];
```

这个方法将 `myWindow` 放到最前面并设为键窗口。

#### 对比总结

| 方法                       | 平台        | 作用                                    | 典型使用场景                                      |
| ------------------------ | --------- | ------------------------------------- | ------------------------------------------- |
| `becomeKey()`            | iOS/macOS | 使窗口成为键窗口，接受事件                         | 在 iOS 中用于 `UIWindow`，在 macOS 中用于 `NSWindow` |
| `makeKey()`              | macOS     | 将窗口设置为键窗口并将其置于最前面（通常是 `NSWindow` 的方法） | 在 macOS 中使用，确保窗口在最前面并能接受事件                  |
| `makeKeyAndOrderFront()` | macOS     | 将窗口设置为键窗口并置于最前面（常见用法，实际做了两件事）         | 在 macOS 中常用，通常用于确保窗口弹出并获取焦点                 |

#### 主要区别：

1. **`becomeKey()`** 主要用于设置窗口成为键窗口，通常用于 iOS 中的 `UIWindow`，或者 macOS 中的 `NSWindow`。
2. **`makeKey()`** 是 macOS 的特有方法，用来将窗口设为键窗口并把它置于最前面，通常在 `NSWindow` 中使用。这个方法通常与 `makeKeyAndOrderFront()` 一起使用，后者会将窗口置前并使其成为键窗口。

总的来说，在 macOS 中，你经常会看到 `makeKeyAndOrderFront()` 被用于确保窗口在最前面并成为键窗口；在 iOS 中，`becomeKey()` 用来管理 `UIWindow` 的键视图状态。
