# 协议

理解不同协议的继承关系及其使用场景。

Swift 协议是用于定义方法、属性和其他需求的蓝图。常见的系统提供的协议包括：

1. **`Equatable`**：用于定义相等性比较的协议。
2. **`Comparable`**：用于定义顺序比较的协议，继承自 `Equatable`。
3. **`Hashable`**：提供对象生成哈希值的能力，继承自 `Equatable`。
4. **`Codable`**：用于将类型编码和解码的协议，结合了 `Encodable` 和 `Decodable`。
5. **`CustomStringConvertible`**：提供类型自定义输出字符串描述的协议。
6. **`Sequence`**、**`Collection`** 和 **`IteratorProtocol`**：定义集合类型的基础协议。
7. **`Error`**：用于定义可以表示错误的类型。





## 小结：

**`Comparable —— Equatable`**

**`Hashable —— Equatable`**

**`Codable —— <`**`Encodable, Decodable`**`>`**

**`CustomStringConvertible`**

**`Sequence`**、**`Collection`** 和 **`IteratorProtocol`**：定义集合类型的基础协议。

**`Error`**
