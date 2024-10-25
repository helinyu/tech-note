# ActivationPolicy

`NSApplication.ActivationPolicy` 有以下几种策略：

1. **`regular`**：这是默认策略，应用程序将显示在 Dock 中，并且可以有主窗口。适用于大多数常规应用程序。
2. **`accessory`**：应用程序作为辅助工具运行，不会在 Dock 中显示，通常不需要主窗口。适合于状态栏应用或小工具，用户通过菜单栏图标与应用程序交互。
3. **`prohibited`**：应用程序不允许在 Dock 中显示，也不允许显示任何窗口。此策略通常用于某些背景服务或工具。

