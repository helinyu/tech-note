# 优先队列

```
MaxPriorityQueue 大顶堆/ 大优先队列
MinPriorityQueue 小顶堆/ 小优先队列
```



## 基本功能



### 0、初始化空队列

```
const maxPQ = new MaxPriorityQueue();
```



### 1、插入队列

**`enqueue(element, priority)`**

* **描述**：将元素插入到优先队列中，并指定其优先级。
* **参数**：
  * `element`：要插入的元素。
  * `priority`：该元素的优先级（可选，默认为元素的值）。

```
   maxPQ.enqueue(3);
   maxPQ.enqueue(1, 10);
   maxPQ.enqueue(5, 20);
```

### 2、弹出队列顶点元素

**`dequeue()`**

* **描述**：移除并返回优先队列中优先级最高的元素。
* **返回值**：包含被移除元素的对象 `{ element, priority }`。

```
   const maxElement = maxPQ.dequeue().element;
   console.log(maxElement);  // 输出：5
```

### 3、获取队列中优先级最高的元素

**`front()`**

* **描述**：返回优先队列中优先级最高的元素，但不移除它。
* **返回值**：包含优先级最高元素的对象 `{ element, priority }`。

```
   const frontElement = maxPQ.front().element;
   console.log(frontElement);  // 输出：5
```

### 4、是否为空

**`isEmpty()`**

* **描述**：检查优先队列是否为空。
* **返回值**：布尔值，`true` 表示队列为空，`false` 表示队列不为空。

```
   const isEmpty = maxPQ.isEmpty();
   console.log(isEmpty);  // 输出：false
```

### 5、大小

**`size()`**

* **描述**：返回优先队列中元素的数量。
* **返回值**：优先队列中元素的数量。

```
   const size = maxPQ.size();
   console.log(size);  // 输出：
```
