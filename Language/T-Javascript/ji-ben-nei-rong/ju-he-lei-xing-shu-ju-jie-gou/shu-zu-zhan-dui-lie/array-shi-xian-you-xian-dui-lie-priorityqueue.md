---
description: Array
---

# Array实现优先队列(priority\_queue)

JavaScript 并没有原生的优先队列（Priority Queue）实现，但你可以通过使用数组和自定义比较函数来实现优先队列的行为。优先队列是一种特殊的队列，其中每个元素都有一个与之相关的优先级，出队时总是优先级最高的元素被移除。

通常可以通过**最小堆**或**最大堆**来实现优先队列，以下是用 JavaScript 实现优先队列的几种方法。

#### 1. **简单的数组实现**

最简单的优先队列可以通过一个数组来存储元素，并且在插入时按照优先级进行排序。

```js
class PriorityQueue {
    constructor() {
        this.queue = [];
    }

    // 插入元素并排序
    enqueue(element, priority) {
        this.queue.push({ element, priority });
        this.queue.sort((a, b) => a.priority - b.priority); // 根据优先级排序，最小优先级在前
    }

    // 移除优先级最高的元素（即优先级最小的）
    dequeue() {
        return this.queue.shift();  // 移除第一个元素
    }

    // 查看队列是否为空
    isEmpty() {
        return this.queue.length === 0;
    }

    // 查看优先级最高的元素
    peek() {
        return this.queue.length > 0 ? this.queue[0] : null;
    }
}

// 示例使用
let pq = new PriorityQueue();
pq.enqueue("Task 1", 2);
pq.enqueue("Task 2", 1);
pq.enqueue("Task 3", 3);

console.log(pq.dequeue()); // { element: 'Task 2', priority: 1 }
```

这种实现虽然简单，但是每次插入时需要进行排序，时间复杂度为 O(n log n)。

#### 2. **基于堆的优先队列**

堆是一种高效实现优先队列的方式，使用最小堆或最大堆可以使插入和删除操作的时间复杂度为 O(log n)。这里使用二叉堆来实现优先队列。

**最小堆实现**

```js
class MinHeap {
    constructor() {
        this.heap = [];
    }

    getParentIndex(i) {
        return Math.floor((i - 1) / 2);
    }

    getLeftChildIndex(i) {
        return 2 * i + 1;
    }

    getRightChildIndex(i) {
        return 2 * i + 2;
    }

    swap(i1, i2) {
        [this.heap[i1], this.heap[i2]] = [this.heap[i2], this.heap[i1]];
    }

    // 插入元素到堆中
    insert(element) {
        this.heap.push(element);
        this.heapifyUp();
    }

    // 上移操作，维持堆的性质
    heapifyUp() {
        let index = this.heap.length - 1;
        while (this.getParentIndex(index) >= 0 && this.heap[this.getParentIndex(index)].priority > this.heap[index].priority) {
            this.swap(this.getParentIndex(index), index);
            index = this.getParentIndex(index);
        }
    }

    // 移除堆顶元素
    remove() {
        if (this.heap.length === 1) return this.heap.pop();
        const root = this.heap[0];
        this.heap[0] = this.heap.pop();
        this.heapifyDown();
        return root;
    }

    // 下移操作，维持堆的性质
    heapifyDown() {
        let index = 0;
        while (this.getLeftChildIndex(index) < this.heap.length) {
            let smallerChildIndex = this.getLeftChildIndex(index);
            if (this.getRightChildIndex(index) < this.heap.length && this.heap[this.getRightChildIndex(index)].priority < this.heap[smallerChildIndex].priority) {
                smallerChildIndex = this.getRightChildIndex(index);
            }

            if (this.heap[index].priority <= this.heap[smallerChildIndex].priority) break;

            this.swap(index, smallerChildIndex);
            index = smallerChildIndex;
        }
    }

    // 查看堆顶元素
    peek() {
        return this.heap[0];
    }

    // 检查堆是否为空
    isEmpty() {
        return this.heap.length === 0;
    }
}

// 使用优先级队列
class PriorityQueue {
    constructor() {
        this.minHeap = new MinHeap();
    }

    enqueue(element, priority) {
        this.minHeap.insert({ element, priority });
    }

    dequeue() {
        return this.minHeap.remove();
    }

    peek() {
        return this.minHeap.peek();
    }

    isEmpty() {
        return this.minHeap.isEmpty();
    }
}

// 示例
let pq = new PriorityQueue();
pq.enqueue("Task 1", 2);
pq.enqueue("Task 2", 1);
pq.enqueue("Task 3", 3);

console.log(pq.dequeue()); // { element: 'Task 2', priority: 1 }
```

这种基于堆的实现，插入和移除操作的时间复杂度是 O(log n)，更高效。

#### 3. **第三方库**

如果你不想自己实现优先队列，可以使用一些成熟的第三方库，例如：

* **`js-priority-queue`**：轻量级的优先队列实现，基于堆。
* **`heap.js`**：专门用于高效堆操作的库。

#### 总结：

* 如果你想自己实现，可以使用数组和排序的方式来实现简单的优先队列。
* 更高效的方式是基于最小堆或最大堆来实现，插入和删除操作的复杂度是 O(log n)。
* 也可以直接使用第三方库，简化工作。
