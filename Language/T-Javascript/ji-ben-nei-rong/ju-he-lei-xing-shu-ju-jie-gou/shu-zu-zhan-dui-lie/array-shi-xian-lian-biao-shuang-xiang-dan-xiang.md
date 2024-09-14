# Array 实现链表（双向、单向）

在 JavaScript 中，没有直接对应于 C++ 中的 `list` 和 `forward_list` 结构的数据类型。不过，可以通过 JavaScript 的 **`Array`** 以及 **自定义类** 来模拟这些结构的行为。

## 1. **C++ `list` 与 `forward_list` 简介**

* **C++ `list`**：是一个双向链表结构，每个节点包含指向前后两个节点的指针，因此可以进行高效的插入、删除等操作。
* **C++ `forward_list`**：是一个单向链表结构，每个节点只包含指向下一个节点的指针，通常比 `list` 更节省空间，但操作也有限制。

## 2. **JavaScript 的 `Array` 代替 `list`**

虽然 JavaScript 中的 `Array` 并不是链表结构，它是基于索引的动态数组，但它提供了足够多的方法来模拟类似 `list` 的操作，比如插入、删除、遍历等。对于大多数应用场景，`Array` 可以胜任。

```js
let arr = [1, 2, 3, 4];
arr.push(5);    // 添加元素到末尾
arr.shift();    // 删除头部元素
arr.splice(1, 0, 10);  // 在索引1位置插入元素10
```

## 3. **使用 JavaScript 自定义类模拟链表**

如果需要像 C++ 的 `list` 和 `forward_list` 一样的链表结构，可以使用 JavaScript 自定义类来实现双向链表和单向链表。

**单向链表 (`forward_list`) 示例**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
  }

  // 在链表末尾添加元素
  append(value) {
    const newNode = new Node(value);
    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  // 删除链表中的第一个元素
  removeHead() {
    if (this.head) {
      this.head = this.head.next;
    }
  }

  // 打印链表
  printList() {
    let current = this.head;
    let list = [];
    while (current) {
      list.push(current.value);
      current = current.next;
    }
    console.log(list.join(' -> '));
  }
}

// 使用单向链表
let list = new SinglyLinkedList();
list.append(1);
list.append(2);
list.append(3);
list.printList();  // 输出: 1 -> 2 -> 3
list.removeHead();
list.printList();  // 输出: 2 -> 3
```

**双向链表 (`list`) 示例**

```js
class DoublyNode {
  constructor(value) {
    this.value = value;
    this.prev = null;
    this.next = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  // 在链表末尾添加元素
  append(value) {
    const newNode = new DoublyNode(value);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
      this.tail = newNode;
    }
  }

  // 删除链表中的最后一个元素
  removeTail() {
    if (this.tail) {
      if (this.tail === this.head) {
        this.head = null;
        this.tail = null;
      } else {
        this.tail = this.tail.prev;
        this.tail.next = null;
      }
    }
  }

  // 打印链表
  printList() {
    let current = this.head;
    let list = [];
    while (current) {
      list.push(current.value);
      current = current.next;
    }
    console.log(list.join(' <-> '));
  }
}

// 使用双向链表
let dll = new DoublyLinkedList();
dll.append(1);
dll.append(2);
dll.append(3);
dll.printList();  // 输出: 1 <-> 2 <-> 3
dll.removeTail();
dll.printList();  // 输出: 1 <-> 2
```

## 4. **总结**

* JavaScript 中没有原生的链表结构，但可以通过数组实现大部分功能。
* 如果需要类似 `list` 或 `forward_list` 的链表结构，可以使用 JavaScript 自定义类进行实现。
