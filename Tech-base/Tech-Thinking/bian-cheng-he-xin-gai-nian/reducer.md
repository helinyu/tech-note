# Reducer

在编程中，**Reducer** 是一种函数模式，通常用于**状态管理**。它接受两个参数：**当前状态**和一个**动作**（Action），并根据动作的类型决定如何更新并返回一个**新状态**。Reducer 的核心特点是其**纯函数**性质，意味着相同的输入总会产生相同的输出，没有副作用。

Reducer 通常用于状态管理库中，例如在 **Redux**（用于 React 应用的状态管理库）中起着核心作用。Reducer 帮助将应用程序的状态和状态更新逻辑集中在一个地方，保证状态变更的可预测性和稳定性。

#### Reducer的核心概念

1. **纯函数**：Reducer 需要是一个纯函数。它不依赖外部状态，且不会修改输入对象。
2. **参数**：
   * **状态**（State）：表示当前的应用状态，通常是一个对象或数据结构。
   * **动作**（Action）：表示引起状态变更的事件。通常是一个包含 `type` 属性的对象，用来指示要进行的操作。
3. **返回新状态**：根据传入的动作类型，Reducer 返回一个新的状态对象。

#### 代码示例

以下是一个简单的 JavaScript Reducer 示例，用于管理计数器的状态：

```javascript
function counterReducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

// 使用示例
const initialState = { count: 0 };
const incrementAction = { type: 'increment' };
const newState = counterReducer(initialState, incrementAction); // { count: 1 }
```

#### Reducer的应用场景

* **状态管理**：在 Redux、React Context 等状态管理工具中，用于更新全局状态。
* **函数式编程**：在 JavaScript 的 `.reduce()` 方法中实现复杂的累加逻辑。
