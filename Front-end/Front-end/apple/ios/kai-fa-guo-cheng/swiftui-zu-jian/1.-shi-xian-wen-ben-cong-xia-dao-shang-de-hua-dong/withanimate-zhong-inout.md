# withAnimate 中inout

在 SwiftUI 中，withAnimation 是一个用于显式触发动画的函数。它的参数是一个 Animation 对象，用于定义动画的持续时间、速度曲线和其他行为。easeInOut 是其中一种常见的速度曲线（timing function），用于控制动画的加速和减速。

***

#### 1. \*\*easeInOut 的作用\*\* <a href="#jeys-1737557374160" id="jeys-1737557374160"></a>

easeInOut 是一种速度曲线，表示动画在开始时会逐渐加速（ease-in），在结束时会逐渐减速（ease-out）。它的特点是：

* \*\*开始和结束较慢\*\*：动画的开始和结束阶段速度较慢。
* \*\*中间较快\*\*：动画的中间阶段速度较快。

这种曲线非常适合用于大多数用户界面动画，因为它看起来更加自然和流畅。

***

#### 2. \*\*其他常见的速度曲线\*\* <a href="#dxpf-1737557374172" id="dxpf-1737557374172"></a>

SwiftUI 提供了多种内置的速度曲线，适用于不同的动画场景。以下是一些常见的速度曲线：

**（1）\*\*linear\*\***

* \*\*线性动画\*\*：动画以恒定速度运行，没有加速或减速。
* 示例：

```
withAnimation(.linear(duration: 0.5)) {
    showView.toggle()
}
```

**（2）\*\*easeIn\*\***

* \*\*缓入动画\*\*：动画开始时较慢，然后逐渐加速。
* 示例：

```
withAnimation(.easeIn(duration: 0.5)) {
    showView.toggle()
}
```

**（3）\*\*easeOut\*\***

* \*\*缓出动画\*\*：动画开始时较快，然后逐渐减速。
* 示例：

```
withAnimation(.easeOut(duration: 0.5)) {
    showView.toggle()
}
```

**（4）\*\*easeInOut\*\***

* \*\*缓入缓出动画\*\*：动画开始和结束时较慢，中间较快。
* 示例：

```
withAnimation(.easeInOut(duration: 0.5)) {
    showView.toggle()
}
```

**（5）\*\*spring\*\***

* \*\*弹簧动画\*\*：动画具有弹性效果，类似于弹簧的振动。
* 示例：

```
withAnimation(.spring(response: 0.5, dampingFraction: 0.6, blendDuration: 0)) {
    showView.toggle()
}
```

**（6）\*\*interactiveSpring\*\***

* \*\*交互式弹簧动画\*\*：类似于 spring，但更适合用户交互（例如拖动）。
* 示例：

```
withAnimation(.interactiveSpring(response: 0.5, dampingFraction: 0.6, blendDuration: 0)) {
    showView.toggle()
}
```

**（7）\*\*default\*\***

* \*\*默认动画\*\*：使用系统默认的动画曲线（通常是 easeInOut）。
* 示例：

```
withAnimation(.default) {
    showView.toggle()
}
```

***

#### 3. \*\*自定义动画\*\* <a href="#fnen-1737557374290" id="fnen-1737557374290"></a>

除了内置的速度曲线，你还可以通过 Animation.timingCurve 自定义动画的速度曲线。它接受四个参数，用于定义三次贝塞尔曲线的控制点：withAnimation(.timingCurve(0.25, 0.1, 0.25, 1, duration: 0.5)) { showView.toggle() }

* 参数 0.25, 0.1, 0.25, 1 是贝塞尔曲线的控制点。
* duration 是动画的持续时间。

***

#### 4. \*\*示例代码\*\* <a href="#tycg-1737557374308" id="tycg-1737557374308"></a>

以下是一个完整的示例，展示了如何使用不同的速度曲线：

```
import SwiftUI

struct AnimationExampleView: View {
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
                    .transition(.opacity)
            }

            Button(showView ? "Hide View" : "Show View") {
                withAnimation(.easeInOut(duration: 0.5)) {
                    showView.toggle()
                }
            }
            .padding()

            Button("Linear Animation") {
                withAnimation(.linear(duration: 0.5)) {
                    showView.toggle()
                }
            }
            .padding()

            Button("Spring Animation") {
                withAnimation(.spring(response: 0.5, dampingFraction: 0.6, blendDuration: 0)) {
                    showView.toggle()
                }
            }
            .padding()
        }
    }
}
```

***

#### 5. \*\*总结\*\* <a href="#yc0v-1737557374397" id="yc0v-1737557374397"></a>

* \*\*easeInOut\*\*：动画开始和结束时较慢，中间较快，适合大多数 UI 动画。
* \*\*其他速度曲线\*\*：linear、easeIn、easeOut、spring、interactiveSpring 等，适用于不同的动画场景。
* \*\*自定义动画\*\*：通过 Animation.timingCurve 可以定义自定义的速度曲线。

根据你的需求选择合适的动画曲线，可以让界面动画更加自然和流畅。
