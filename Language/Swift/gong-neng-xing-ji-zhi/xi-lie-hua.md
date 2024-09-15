# 系列化（

在 Swift 中，**序列化**（Serialization）是将对象或数据结构转换为可以存储或传输的格式的过程。最常见的用途是将对象转换为 JSON 或者 Plist 格式，以便将其保存到文件、发送到服务器，或者从网络响应中解析。

Swift 提供了几种方式进行序列化和反序列化，其中最常见的是使用 `Codable` 协议和 `JSONEncoder` / `JSONDecoder` 来处理 JSON 数据。下面是关于 Swift 中序列化的详细介绍。

#### 1. 使用 `Codable` 进行 JSON 序列化

`Codable` 是 Swift 提供的一个协议，它结合了 `Encodable` 和 `Decodable` 协议，使得对象可以很方便地进行序列化（编码）和反序列化（解码）。通过实现 `Codable` 协议，结构体或类可以轻松地与 JSON 进行互操作。

**示例：定义 `Codable` 结构体**

```swift
struct User: Codable {
    var name: String
    var age: Int
    var email: String
}
```

在这个例子中，`User` 结构体自动遵循 `Codable` 协议，Swift 会为其生成序列化和反序列化代码。

**示例：序列化（对象转 JSON）**

```swift
let user = User(name: "Alice", age: 25, email: "alice@example.com")

let encoder = JSONEncoder()
encoder.outputFormatting = .prettyPrinted  // 格式化输出以便更容易阅读

if let jsonData = try? encoder.encode(user) {
    if let jsonString = String(data: jsonData, encoding: .utf8) {
        print(jsonString)
    }
}
```

输出结果：

```json
{
  "name" : "Alice",
  "age" : 25,
  "email" : "alice@example.com"
}
```

**示例：反序列化（JSON 转对象）**

```swift
let jsonString = """
{
  "name": "Alice",
  "age": 25,
  "email": "alice@example.com"
}
"""

if let jsonData = jsonString.data(using: .utf8) {
    let decoder = JSONDecoder()
    if let user = try? decoder.decode(User.self, from: jsonData) {
        print(user)
    }
}
```

输出结果：

```
User(name: "Alice", age: 25, email: "alice@example.com")
```

#### 2. 使用 `Codable` 进行 Plist 序列化

除了 JSON，Swift 还可以使用 `Codable` 协议将对象序列化为 Plist 格式（属性列表）。Plist 是一种 XML 格式，常用于在 iOS 和 macOS 中存储数据。

**示例：Plist 序列化**

```swift
let encoder = PropertyListEncoder()
encoder.outputFormat = .xml

if let plistData = try? encoder.encode(user) {
    if let plistString = String(data: plistData, encoding: .utf8) {
        print(plistString)
    }
}
```

输出结果（Plist 格式）：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>age</key>
    <integer>25</integer>
    <key>email</key>
    <string>alice@example.com</string>
    <key>name</key>
    <string>Alice</string>
</dict>
</plist>
```

**示例：Plist 反序列化**

```swift
let decoder = PropertyListDecoder()
if let userFromPlist = try? decoder.decode(User.self, from: plistData) {
    print(userFromPlist)
}
```

#### 3. 自定义编码和解码

有时候，自动生成的 `Codable` 实现不能满足需求（例如，字段名不同或需要进行某些转换）。在这种情况下，你可以通过实现 `Encodable` 和 `Decodable` 协议来自定义序列化和反序列化过程。

**示例：自定义编码和解码**

```swift
struct User: Codable {
    var name: String
    var age: Int
    var email: String
    
    enum CodingKeys: String, CodingKey {
        case name
        case age
        case email = "user_email"  // 将 "email" 映射到 "user_email"
    }
    
    func encode(to encoder: Encoder) throws {
        var container = encoder.container(keyedBy: CodingKeys.self)
        try container.encode(name, forKey: .name)
        try container.encode(age, forKey: .age)
        try container.encode(email, forKey: .email)
    }
    
    init(from decoder: Decoder) throws {
        let container = try decoder.container(keyedBy: CodingKeys.self)
        name = try container.decode(String.self, forKey: .name)
        age = try container.decode(Int.self, forKey: .age)
        email = try container.decode(String.self, forKey: .email)
    }
}
```

在这个例子中，`email` 字段在 JSON 中表示为 `user_email`，但在代码中仍然使用 `email` 字段。通过自定义 `CodingKeys` 枚举，可以将 JSON 的字段名映射到结构体的属性名。

#### 4. 使用 `NSCoding` 进行序列化

在一些需要与 Objective-C 兼容的场景下，Swift 也可以使用 `NSCoding` 协议进行序列化。`NSCoding` 主要用于归档和解档对象。

**示例：`NSCoding` 序列化**

```swift
class Person: NSObject, NSCoding {
    var name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    required init?(coder aDecoder: NSCoder) {
        name = aDecoder.decodeObject(forKey: "name") as! String
        age = aDecoder.decodeInteger(forKey: "age")
    }
    
    func encode(with aCoder: NSCoder) {
        aCoder.encode(name, forKey: "name")
        aCoder.encode(age, forKey: "age")
    }
}
```

#### 5. 使用 `Codable` 序列化嵌套对象

当你的对象中包含其他对象时，`Codable` 也能处理嵌套的结构。

**示例：嵌套对象的序列化**

```swift
struct Address: Codable {
    var street: String
    var city: String
}

struct User: Codable {
    var name: String
    var age: Int
    var address: Address
}

let address = Address(street: "123 Main St", city: "New York")
let user = User(name: "Alice", age: 25, address: address)

let encoder = JSONEncoder()
if let jsonData = try? encoder.encode(user),
   let jsonString = String(data: jsonData, encoding: .utf8) {
    print(jsonString)
}
```

#### 6. 错误处理

在序列化和反序列化过程中，可能会出现错误，比如数据格式不匹配或丢失。Swift 使用 `try`、`catch` 处理这些错误。

**示例：错误处理**

```swift
do {
    let jsonData = try encoder.encode(user)
} catch {
    print("Failed to encode user: \(error.localizedDescription)")
}
```

#### 总结

Swift 提供了强大且灵活的序列化功能，最常用的是通过 `Codable` 处理 JSON 和 Plist 数据。通过使用 `Codable`，开发者可以轻松地在对象和外部数据格式之间进行转换，并且 Swift 提供了自定义编码和解码的选项来处理更复杂的数据结构。
