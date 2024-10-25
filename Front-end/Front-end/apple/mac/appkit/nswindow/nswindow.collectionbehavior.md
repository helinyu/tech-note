# NSWindow.CollectionBehavior

`NSWindow` 中的 `collectionBehavior` 是一个属性，用于指定窗口如何在 macOS 中处理某些集合行为（collection behaviors），例如在全屏模式、多显示器、应用程序间切换等情况下的行为。

`collectionBehavior` 的类型是 `NSWindow.CollectionBehavior`，它是一个选项集（`OptionSet`），允许组合多个行为。通过设置这个属性，你可以自定义窗口在不同使用场景下的表现方式。

常见的 `NSWindow.CollectionBehavior` 值包括：

1. **.default**: 窗口使用系统默认的集合行为。
2. **.canJoinAllSpaces**: 窗口可以出现在所有的桌面空间（Spaces）上。
3. **.moveToActiveSpace**: 当用户切换到另一个空间时，窗口会自动跟随用户的焦点移动到当前活跃空间。
4. **.managed**: 窗口遵循常规的空间和全屏管理策略。
5. **.transient**: 窗口是临时窗口，当空间切换时，它会被关闭而不保留在当前空间。
6. **.stationary**: 窗口不会跟随用户的活动空间切换。
7. **.participatesInCycle**: 窗口将参与 Command-Tab 应用切换和其他窗口切换。
8. **.ignoresCycle**: 窗口将不会参与应用的窗口切换。
9. **.fullScreenPrimary**: 窗口可以成为全屏模式的主窗口。
10. **.fullScreenAuxiliary**: 窗口可以成为全屏模式下的辅助窗口（例如在 Split View 中）。

使用示例：

```swift
window.collectionBehavior = [.fullScreenPrimary, .canJoinAllSpaces]
```

这行代码设置了窗口允许进入全屏模式并可以显示在所有桌面空间上。

通过调整 `collectionBehavior`，你可以控制窗口在不同情境下的显示和行为，改善用户体验。
