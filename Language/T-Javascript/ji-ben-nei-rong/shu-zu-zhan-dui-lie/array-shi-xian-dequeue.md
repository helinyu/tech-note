# Array实现dequeue

在 JavaScript 中没有与 C++中的 `deque`（双端队列）完全对应的内置数据结构，但可以通过数组模拟类似的功能。

1. **模拟双端队列的操作**：
   * 在数组头部添加元素可以使用 `unshift` 方法，类似 `deque` 的 `push_front`。
   * 在数组尾部添加元素可以使用 `push` 方法，类似 `deque` 的 `push_back`。
   * 从数组头部移除元素可以使用 `shift` 方法，类似 `deque` 的 `pop_front`。
   * 从数组尾部移除元素可以使用 `pop` 方法，类似 `deque` 的 `pop_back`。

以下是一个示例：

```javascript
let myDequeLikeArray = [];

// 模拟 push_back
myDequeLikeArray.push(10);
myDequeLikeArray.push(20);

// 模拟 push_front
myDequeLikeArray.unshift(5);

console.log(myDequeLikeArray); // [5, 10, 20]

// 模拟 pop_back
let poppedBack = myDequeLikeArray.pop();
console.log(poppedBack); // 20
console.log(myDequeLikeArray); // [5, 10]

// 模拟 pop_front
let poppedFront = myDequeLikeArray.shift();
console.log(poppedFront); // 5
console.log(myDequeLikeArray); // [10]
```

虽然可以通过数组模拟一些双端队列的操作，但在性能和功能上可能与 C++的 `deque` 有一定差距。如果需要更强大的类似功能，可以考虑使用一些 JavaScript 的库，如 `lodash` 等，它们可能提供了更丰富的数据结构和操作方法。
