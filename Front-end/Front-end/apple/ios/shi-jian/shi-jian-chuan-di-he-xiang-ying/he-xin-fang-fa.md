# 核心方法

在 iOS 中，`hitTest(_:with:)` 和 `point(inside:with:)` 是处理触摸事件传递的两个关键方法。它们经常一起使用，但有不同的作用和工作原理。以下是它们的详细解释和区别：

#### 1. `hitTest(_:with:)`

**作用**

`hitTest(_:with:)` 是用来确定哪个视图应该响应触摸事件的。它会在视图层次结构中进行递归查找，最终找到最合适的视图来处理事件。

**工作原理**

* 当用户触摸屏幕时，系统从视图的最顶层（如 `UIWindow`）开始调用 `hitTest(_:with:)`，遍历每个子视图来找到最合适的视图。
* 通过 `hitTest(_:with:)`，系统可以确定触摸事件的目标视图，并将事件交给该视图处理。

**执行过程**

* 调用 `point(inside:with:)` 方法来确定触摸点是否在当前视图内。
* 如果触摸点在当前视图内，则递归检查所有子视图，找到最靠近触摸点的、可以响应事件的子视图。
* 最后返回能够处理事件的视图。

**示例代码**

```swift
override func hitTest(_ point: CGPoint, with event: UIEvent?) -> UIView? {
    if !self.isUserInteractionEnabled || self.isHidden || self.alpha < 0.01 {
        return nil
    }
    if self.point(inside: point, with: event) {
        for subview in self.subviews.reversed() {
            let convertedPoint = subview.convert(point, from: self)
            if let hitView = subview.hitTest(convertedPoint, with: event) {
                return hitView
            }
        }
        return self
    }
    return nil
}
```

在这个例子中，`hitTest(_:with:)` 会检查每个子视图，并根据视图是否能处理事件返回适当的视图。

#### 2. `point(inside:with:)`

**作用**

`point(inside:with:)` 方法用于判断一个触摸点是否位于当前视图的边界内。它只检查给定的点是否在当前视图的范围中，不做其他任何事件处理。

**工作原理**

* `point(inside:with:)` 方法的返回值是一个布尔值。如果触摸点在当前视图的边界内，它返回 `true`，否则返回 `false`。
* 该方法通常在 `hitTest(_:with:)` 内部被调用，用于辅助确定触摸事件的目标视图。

**执行过程**

* 检查触摸点是否在当前视图的范围内。视图的范围通常由视图的 `bounds` 属性决定。
* 如果点在范围内，返回 `true`，否则返回 `false`。

**示例代码**

```swift
override func point(inside point: CGPoint, with event: UIEvent?) -> Bool {
    let isInside = self.bounds.contains(point)
    return isInside
}
```

#### 区别总结

* **`hitTest(_:with:)`**：
  * 用来确定触摸事件的目标视图。
  * 它在视图层次结构中递归查找，最终返回能够处理事件的视图。
  * `hitTest(_:with:)` 调用 `point(inside:with:)` 来帮助判断点是否在视图内。
* **`point(inside:with:)`**：
  * 用来判断触摸点是否在当前视图的范围内。
  * 只做简单的几何判断，返回一个布尔值。
  * 这个方法通常在 `hitTest(_:with:)` 中被调用，不会单独用于事件传递的最终决策。

#### `hitTest(_:with:)` 和 `point(inside:with:)` 的关系

* **`hitTest(_:with:)`** 是触摸事件传递的主入口方法，它依赖 **`point(inside:with:)`** 来判断触摸点是否在视图范围内。
* 当一个视图接收到触摸事件时，首先会调用 **`point(inside:with:)`** 来判断事件是否发生在视图内。如果返回 `true`，则 `hitTest(_:with:)` 继续检查子视图；否则直接返回 `nil`。

#### 应用场景

* **`hitTest(_:with:)`** 主要用于自定义事件传递行为。例如，如果你希望事件传递给视图之外的区域，或者希望在特定条件下阻止事件传递，可以重写 `hitTest(_:with:)`。
* **`point(inside:with:)`** 通常用于改变视图的点击区域。例如，你可以通过重写这个方法来扩大或缩小视图的点击区域。

#### 总结

* `hitTest(_:with:)` 用于确定哪个视图响应触摸事件，依赖 `point(inside:with:)` 判断触摸点是否在视图的边界内。
* `point(inside:with:)` 是一个辅助方法，它只做几何判断，并不决定事件传递逻辑。
