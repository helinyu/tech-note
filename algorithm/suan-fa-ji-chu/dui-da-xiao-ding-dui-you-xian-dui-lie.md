# 堆（大/小顶堆 、优先队列）



大顶堆、小顶堆

优先队列 是基于堆来实现的

## 1、大顶堆（Max-Heap）实现

```swift
struct MaxHeap<T: Comparable> {
    private var heap = [T]()

    mutating func insert(_ value: T) {
        heap.append(value)
        siftUp(from: heap.count - 1)
    }

    mutating func extractMax() -> T? {
        guard !heap.isEmpty else { return nil }
        if heap.count == 1 {
            return heap.removeFirst()
        } else {
            let max = heap[0]
            heap[0] = heap.removeLast()
            siftDown(from: 0)
            return max
        }
    }

    private mutating func siftUp(from index: Int) {
        var child = index
        var parent = (child - 1) / 2
        while child > 0 && heap[child] > heap[parent] {
            heap.swapAt(child, parent)
            child = parent
            parent = (child - 1) / 2
        }
    }

    private mutating func siftDown(from index: Int) {
        var parent = index
        while true {
            let left = 2 * parent + 1
            let right = 2 * parent + 2
            var candidate = parent
            if left < heap.count && heap[left] > heap[candidate] {
                candidate = left
            }
            if right < heap.count && heap[right] > heap[candidate] {
                candidate = right
            }
            if candidate == parent {
                return
            }
            heap.swapAt(parent, candidate)
            parent = candidate
        }
    }
}

// 使用示例
var maxHeap = MaxHeap<Int>()
maxHeap.insert(3)
maxHeap.insert(1)
maxHeap.insert(5)
maxHeap.insert(2)

while let max = maxHeap.extractMax() {
    print(max)  // 输出：5 3 2 1
}
```

## 小顶堆（Min-Heap）实现

```swift
struct MinHeap<T: Comparable> {
    private var heap = [T]()

    mutating func insert(_ value: T) {
        heap.append(value)
        siftUp(from: heap.count - 1)
    }

    mutating func extractMin() -> T? {
        guard !heap.isEmpty else { return nil }
        if heap.count == 1 {
            return heap.removeFirst()
        } else {
            let min = heap[0]
            heap[0] = heap.removeLast()
            siftDown(from: 0)
            return min
        }
    }

    private mutating func siftUp(from index: Int) {
        var child = index
        var parent = (child - 1) / 2
        while child > 0 && heap[child] < heap[parent] {
            heap.swapAt(child, parent)
            child = parent
            parent = (child - 1) / 2
        }
    }

    private mutating func siftDown(from index: Int) {
        var parent = index
        while true {
            let left = 2 * parent + 1
            let right = 2 * parent + 2
            var candidate = parent
            if left < heap.count && heap[left] < heap[candidate] {
                candidate = left
            }
            if right < heap.count && heap[right] < heap[candidate] {
                candidate = right
            }
            if candidate == parent {
                return
            }
            heap.swapAt(parent, candidate)
            parent = candidate
        }
    }
}

// 使用示例
var minHeap = MinHeap<Int>()
minHeap.insert(3)
minHeap.insert(1)
minHeap.insert(5)
minHeap.insert(2)

while let min = minHeap.extractMin() {
    print(min)  // 输出：1 2 3 5
}
```

#### 总结

大顶堆适用于优先级越大越先处理的场景；

小顶堆适用于优先级越小越先处理的场景；



其实优先队列就是大顶堆和小顶堆，&#x20;

看这个优先队列是让大到小排序还是小到大排序吧了。



