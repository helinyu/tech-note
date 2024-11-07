# @binding vs v-model(Vue)

在 SwiftUI 中的 `@Binding` 和 Vue.js 中的 `v-model` 有相似的目的，都是用于实现数据的双向绑定，但它们的实现和用法有所不同。下面是它们的对比：

| 特性       | `@Binding` (SwiftUI)             | `v-model` (Vue.js)             |
| -------- | -------------------------------- | ------------------------------ |
| **用途**   | 在父视图和子视图之间共享和修改状态                | 实现数据的双向绑定                      |
| **作用域**  | 允许子视图访问和修改父视图的状态                 | 直接绑定到 Vue 实例的状态                |
| **实现方式** | 使用 `$` 符号来创建绑定                   | 使用 `v-model` 指令                |
| **数据更新** | 子视图通过 `@Binding` 修改父视图状态，父视图自动更新 | 当输入值改变时，自动更新绑定的变量              |
| **示例**   | `@Binding var isOn: Bool`        | `<input v-model="inputValue">` |

#### 详细说明

* **@Binding**:
  * 在 SwiftUI 中，子视图使用 `@Binding` 声明一个绑定属性，允许它访问父视图的状态。子视图可以通过这个绑定属性修改状态，导致父视图重新渲染。
* **v-model**:
  * 在 Vue.js 中，`v-model` 用于在输入元素（如 `<input>`、`<textarea>` 等）和 Vue 实例的数据属性之间创建双向绑定。当输入值变化时，相关数据属性自动更新；反之，当数据属性变化时，视图也会更新。

#### 总结

两者都实现了双向数据绑定，但 `@Binding` 更侧重于视图之间的状态共享，而 `v-model` 则专注于视图与数据之间的绑定。