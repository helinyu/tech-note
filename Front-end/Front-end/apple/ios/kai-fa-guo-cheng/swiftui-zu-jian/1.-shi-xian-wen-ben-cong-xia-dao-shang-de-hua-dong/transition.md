# transition

在 SwiftUI 中，.transition 和 .asymmetric 是用于控制视图插入和移除时的动画效果的关键修饰符。以下是对它们的详细解释：

***

#### 1. \*\*.transition\*\* <a href="#id-75gl-1737557168292" id="id-75gl-1737557168292"></a>

.transition 是 SwiftUI 中的一个修饰符，用于定义视图在插入或移除时的过渡动画。它可以与任何符合 Transition 协议的类型一起使用，例如：

* .opacity：淡入淡出。
* .scale：缩放。
* .move(edge:)：从指定边缘滑入或滑出。
* .slide：从边缘滑入或滑出。
* .offset：通过偏移量移动视图。

**示例：**

```
.transition(.opacity) // 淡入淡出
.transition(.scale)   // 缩放
.transition(.move(edge: .bottom)) // 从底部滑入或滑出
```

***

#### 2. \*\*.asymmetric\*\* <a href="#id-5ytc-1737557168319" id="id-5ytc-1737557168319"></a>

.asymmetric 是 Transition 的一个特殊类型，允许你为视图的插入（insertion）和移除（removal）分别指定不同的过渡效果。它的定义如下：

```
static func asymmetric(insertion: Transition, removal: Transition) -> AnyTransition
```

* \*\*insertion\*\*：视图插入时的过渡效果。
* \*\*removal\*\*：视图移除时的过渡效果。

**示例：**

```
.transition(.asymmetric(
    insertion: .move(edge: .bottom), // 插入时从底部滑入
    removal: .move(edge: .top)       // 移除时向顶部滑出
))
```

***

#### 3. \*\*.transition(.asymmetric(insertion: .move(edge: .bottom), removal: .move(edge: .top))) 的含义\*\* <a href="#zyva-1737557168346" id="zyva-1737557168346"></a>

这句话的意思是：

* \*\*插入时\*\*：视图从屏幕底部滑入（insertion: .move(edge: .bottom)）。
* \*\*移除时\*\*：视图向屏幕顶部滑出（removal: .move(edge: .top)）。

这种不对称的过渡效果通常用于创建更自然的动画，例如轮播图、模态视图或列表项的插入和移除。

***

#### 4. \*\*完整示例\*\* <a href="#r3hj-1737557168357" id="r3hj-1737557168357"></a>

```
import SwiftUI

struct TransitionExampleView: View {
    @State private var showView = false

    var body: some View {
        VStack {
            if showView {
                Text("Hello, SwiftUI!")
                    .font(.largeTitle)
                    .padding()
                    .background(Color.blue)
                    .foregroundColor(.white)
                    .cornerRadius(10)
                    .transition(.asymmetric(
                        insertion: .move(edge: .bottom), // 插入时从底部滑入
                        removal: .move(edge: .top)       // 移除时向顶部滑出
                    ))
            }

            Button(showView ? "Hide View" : "Show View") {
                withAnimation(.easeInOut(duration: 0.5)) {
                    showView.toggle()
                }
            }
            .padding()
        }
    }
}
```

***

#### 5. \*\*代码解析\*\* <a href="#balg-1737557168424" id="balg-1737557168424"></a>

* \*\*if showView\*\*：根据 showView 的状态决定是否显示视图。
* \*\*.transition(.asymmetric(...))\*\*：
*
  * 当视图插入时，从底部滑入（insertion: .move(edge: .bottom)）。
  * 当视图移除时，向顶部滑出（removal: .move(edge: .top)）。
* \*\*withAnimation\*\*：在切换 showView 状态时，应用动画效果。

***

#### 6. \*\*常见过渡效果\*\* <a href="#wawx-1737557168438" id="wawx-1737557168438"></a>

以下是一些常见的过渡效果，可以与 .transition 和 .asymmetric 结合使用：

**（1）\*\*move(edge:)\*\***

* 从指定边缘滑入或滑出。
* 示例：

.transition(.move(edge: .leading)) // 从左侧滑入或滑出

**（2）\*\*opacity\*\***

* 淡入淡出。
* 示例：

.transition(.opacity)

**（3）\*\*scale\*\***

* 缩放。
* 示例：

.transition(.scale)

**（4）\*\*slide\*\***

* 从边缘滑入或滑出。
* 示例：

.transition(.slide)

**（5）\*\*offset\*\***

* 通过偏移量移动视图。
* 示例：

.transition(.offset(x: 100, y: 0)) // 水平偏移 100 点

***

#### 7. \*\*总结\*\* <a href="#mlzu-1737557168499" id="mlzu-1737557168499"></a>

* \*\*.transition\*\*：用于定义视图插入或移除时的过渡动画。
* \*\*.asymmetric\*\*：允许为插入和移除分别指定不同的过渡效果。
* \*\*move(edge:)\*\*：从指定边缘滑入或滑出。

通过结合 .transition 和 .asymmetric，你可以创建复杂的、非对称的动画效果，使界面更加生动和自然。
