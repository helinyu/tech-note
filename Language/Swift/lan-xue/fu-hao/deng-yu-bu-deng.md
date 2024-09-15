# 等于不等

\== 和 === 以及!=和!==

字符串在 Swift 中是一个功能强大且灵活的数据类型。以下是一些关于 Swift 字符串的基本操作：

#### 创建字符串

```swift
let greeting = "Hello, World!"
```

#### 拼接字符串

```swift
let firstName = "John"
let lastName = "Doe"
let fullName = "\(firstName) \(lastName)"
```

#### 字符串长度

```swift
let length = greeting.count
```

#### 访问字符串中的字符

```swift
let firstCharacter = greeting[greeting.startIndex]
let lastCharacter = greeting[greeting.index(before: greeting.endIndex)]
```

#### 遍历字符串中的字符

```swift
for character in greeting {
    print(character)
}
```

#### 修改字符串

```swift
var mutableString = "Hello"
mutableString += ", World!"
```

#### 插入和删除字符

```swift
var welcome = "Hello"
welcome.insert("!", at: welcome.endIndex)

welcome.remove(at: welcome.index(before: welcome.endIndex))
```

#### 字符串比较

```swift
let string1 = "Hello"
let string2 = "hello"

if string1 == string2 {
    print("The strings are equal.")
} else {
    print("The strings are not equal.")
}
```

#### 字符串包含子字符串

```swift
let sentence = "The quick brown fox jumps over the lazy dog"
if sentence.contains("fox") {
    print("The sentence contains 'fox'.")
}
```

#### 转换大小写

```swift
let uppercase = greeting.uppercased()
let lowercase = greeting.lowercased()
```

#### 子字符串

```swift
let startIndex = greeting.index(greeting.startIndex, offsetBy: 7)
let endIndex = greeting.index(greeting.startIndex, offsetBy: 12)
let substring = greeting[startIndex..<endIndex]
```

#### 字符串分割

```swift
let words = sentence.split(separator: " ")
for word in words {
    print(word)
}
```

这些都是 Swift 中字符串操作的一些基本示例。希望这些信息对你有帮助！如果你有任何其他问题或需要更详细的解释，请告诉我。



在 Swift 中，`!=` 和 `!==` 也是两个不同的运算符，用于不同的比较目的。

#### `!=` 运算符

`!=` 运算符用于判断两个值是否不相等。它是 `==` 运算符的反义运算符。

```swift
struct Person: Equatable {
    var name: String
}

let personA = Person(name: "John")
let personB = Person(name: "John")
let personC = Person(name: "Doe")

if personA != personB {
    print("personA and personB are not equal.")
} else {
    print("personA and personB are equal.")
}

if personA != personC {
    print("personA and personC are not equal.")
} else {
    print("personA and personC are equal.")
}
```

在这个例子中，`personA` 和 `personB` 的属性值相同，所以 `personA != personB` 结果为 `false`。而 `personA` 和 `personC` 的属性值不同，所以 `personA != personC` 结果为 `true`。

#### `!==` 运算符

`!==` 运算符用于判断两个对象是否不引用同一个实例。它是 `===` 运算符的反义运算符。

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

let person1 = Person(name: "John")
let person2 = Person(name: "John")
let person3 = person1

if person1 !== person2 {
    print("person1 and person2 do not reference the same instance.")
} else {
    print("person1 and person2 reference the same instance.")
}

if person1 !== person3 {
    print("person1 and person3 do not reference the same instance.")
} else {
    print("person1 and person3 reference the same instance.")
}
```

在这个例子中，`person1` 和 `person2` 是两个不同的实例，所以 `person1 !== person2` 结果为 `true`。而 `person1` 和 `person3` 引用同一个实例，所以 `person1 !== person3` 结果为 `false`。

总结一下，`!=` 用于判断两个值是否不相等，而 `!==` 用于判断两个对象是否不引用同一个实例。如果你需要比较值的不同，使用 `!=`；如果你需要判断两个引用是否不同，使用 `!==`。



{% hint style="info" %}
总结

1、== 判断的是值是否相等

2、=== 判断是否是同一个对象，判断指针是否是同一个

3、!= 和 == 相反

4、!== 和 === 相反
{% endhint %}



