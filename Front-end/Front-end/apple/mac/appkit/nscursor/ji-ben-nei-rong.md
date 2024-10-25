# 基本内容

在 macOS 开发中，`NSCursor` 类提供了丰富的属性和方法来管理光标样式。以下是 `NSCursor` 的主要属性和方法的详细介绍：

#### 属性

1. **`current`**
   * **描述**: 获取当前活动的光标。
   *   **用法**:

       ```swift
       let activeCursor = NSCursor.current
       ```

#### 方法

1. **`set()`**
   * **描述**: 将光标设置为当前光标。
   *   **用法**:

       ```swift
       NSCursor.pointingHand.set()
       ```
2. **`image`**
   * **描述**: 返回光标的图像。
   *   **用法**:

       ```swift
       let cursorImage = NSCursor.arrow.image
       ```
3. **`hotSpot`**
   * **描述**: 返回光标的热点位置（光标图像中触发交互的点）。
   *   **用法**:

       ```swift
       let cursorHotSpot = NSCursor.arrow.hotSpot
       ```
4. **`addCursorRect(_:cursor:)`**
   * **描述**: 为特定矩形区域添加光标样式。
   *   **用法**:

       <pre class="language-swift"><code class="lang-swift"><strong>addCursorRect(bounds, cursor: NSCursor.pointingHand)
       </strong></code></pre>
5. **`resetCursorRects()`**
   * **描述**: 在视图的光标区域更新时调用，用于重置光标区域。
   *   **用法**:

       ```swift
       override func resetCursorRects() {
           super.resetCursorRects()
           addCursorRect(bounds, cursor: NSCursor.pointingHand)
       }
       ```
6. **`link`**
   * **描述**: 返回一个表示链接的光标。
   *   **用法**:

       ```swift
       NSCursor.link.set()
       ```
7. **`closedHand`**
   * **描述**: 返回一个表示正在拖动的手形光标。
   *   **用法**:

       ```swift
       NSCursor.closedHand.set()
       ```
8. **`openHand`**
   * **描述**: 返回一个表示可拖动的手形光标。
   *   **用法**:

       ```swift
       NSCursor.openHand.set()
       ```
9. **`crosshair`**
   * **描述**: 返回一个十字形光标，通常用于绘图工具。
   *   **用法**:

       ```swift
       NSCursor.crosshair.set()
       ```
10. **`resizeLeftRight` / `resizeUpDown`**
    * **描述**: 返回表示左右或上下缩放的光标。
    *   **用法**:

        ```swift
        NSCursor.resizeLeftRight.set()
        NSCursor.resizeUpDown.set()
        ```

#### 自定义光标

如果你需要创建自定义光标，可以使用以下方法：

* **`init(image:hotSpot:)`**
  * **描述**: 根据图像和热点位置初始化一个光标。
  *   **用法**:

      ```swift
      let customCursor = NSCursor(image: yourImage, hotSpot: NSPoint(x: 0, y: 0))
      customCursor.set()
      ```

#### 其他方法

* **`hide()` / `unhide()`**
  * **描述**: 隐藏或显示光标。
  *   **用法**:

      ```swift
      NSCursor.hide()
      NSCursor.unhide()
      ```

#### 总结

`NSCursor` 提供了多种方法和属性，用于灵活地控制和管理光标的外观和行为。在开发过程中，合理地使用这些方法和属性可以提升用户交互体验，确保光标样式与应用的功能和上下文相匹配。
