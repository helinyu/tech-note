# Codable协议

`Codable` 协议是 Swift 4 引入的一个协议，用于实现类型的编码和解码。它结合了 `Encodable` 和 `Decodable` 两个协议，允许开发者方便地将 Swift 数据结构与 JSON 数据进行相互转换。以下是对 `Codable` 协议的详细介绍：

#### 1. 基本概念

* **`Encodable`**：允许将数据结构编码为外部表示（如 JSON）。
* **`Decodable`**：允许将外部表示（如 JSON）解码为数据结构。
* **`Codable`**：同时符合 `Encodable` 和 `Decodable` 的协议，简化了这两者的使用。

#### 2. 使用方式

**定义模型**

要使用 `Codable`，你需要定义符合 `Codable` 协议的模型。例如：

```swift
import Foundation

struct User: Codable {
    let id: Int
    let name: String
    let email: String?
}
```

在这个例子中，`User` 结构体包含三个属性，其中 `email` 是可选的。

**JSON 编码**

将一个 `Codable` 类型实例编码为 JSON 的示例：

```swift
let user = User(id: 1, name: "Alice", email: "alice@example.com")

do {
    let jsonData = try JSONEncoder().encode(user)
    let jsonString = String(data: jsonData, encoding: .utf8)!
    print(jsonString)
} catch {
    print("Error encoding JSON: \(error)")
}
```

**JSON 解码**

将 JSON 数据解码为 `Codable` 类型实例的示例：

```swift
let jsonString = """
{
    "id": 1,
    "name": "Alice",
    "email": "alice@example.com"
}
"""

if let jsonData = jsonString.data(using: .utf8) {
    do {
        let user = try JSONDecoder().decode(User.self, from: jsonData)
        print(user)
    } catch {
        print("Error decoding JSON: \(error)")
    }
}
```

#### 3. 处理复杂数据

对于更复杂的 JSON 结构，例如嵌套对象或数组，`Codable` 同样可以轻松处理：

```swift
struct Group: Codable {
    let groupName: String
    let members: [User]
}

let jsonString = """
{
    "groupName": "Developers",
    "members": [
        {"id": 1, "name": "Alice", "email": "alice@example.com"},
        {"id": 2, "name": "Bob", "email": "bob@example.com"}
    ]
}
"""

if let jsonData = jsonString.data(using: .utf8) {
    do {
        let group = try JSONDecoder().decode(Group.self, from: jsonData)
        print(group)
    } catch {
        print("Error decoding JSON: \(error)")
    }
}
```

#### 4. 自定义编码和解码

你可以实现自定义的编码和解码逻辑，通过实现 `encode(to:)` 和 `init(from:)` 方法：

```swift
struct User: Codable {
    let id: Int
    let name: String

    enum CodingKeys: String, CodingKey {
        case id
        case name = "userName"  // 将 "userName" 映射到 `name` 属性
    }
}
```

#### 5. 小结

* `Codable` 是处理 JSON 数据的强大工具，提供了类型安全和编译时检查。
* 适合用于静态和结构化的 JSON 数据，尤其是在数据模型已知的情况下。
* 可以灵活处理复杂和嵌套的 JSON 结构，支持自定义编码和解码。
