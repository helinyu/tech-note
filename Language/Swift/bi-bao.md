# 闭包

可以在代码中捕获和存储变量和常量的功能块。闭包与 C 和 Objective-C 中的块（blocks）以及其他编程语言中的匿名函数或 lambda 表达式类似。**闭包可以在代码中作为值传递或返回，既可以是有名的函数，也可以是无名的（匿名的）表达式。**

## 1、闭包的组成部分（3哥部分）

* **参数列表**：与函数参数类似，用来接收输入值。
* **返回值类型**：定义闭包的返回值类型。
* **代码体**：实现闭包的具体逻辑。

```swift
{ (参数列表) -> 返回类型 in
    执行代码
}
```

* **参数列表**：和函数一样，可以有参数。
* **返回类型**：指定闭包返回的类型。
* **in** 关键字：用于分隔参数列表和闭包体的代码。



## 2、有三种主要形式：

1. 全局函数：有名字，但不能捕获任何值。
2. 嵌套函数：有名字，且可以从其上层函数捕获值。
3. 闭包表达式：无名闭包，可以根据上下文捕获值。

#### \*\* 闭包的使用示例

**无参数、无返回值的闭包**

```swift
swift复制代码let simpleClosure = {
    print("This is a simple closure.")
}

simpleClosure()  // 调用闭包，输出：This is a simple closure.
```

**有参数、无返回值的闭包**

```swift
swift复制代码let greetClosure = { (name: String) in
    print("Hello, \(name)!")
}

greetClosure("Alice")  // 输出：Hello, Alice!
```

**有参数、有返回值的闭包**

```swift
swift复制代码let addClosure = { (a: Int, b: Int) -> Int in
    return a + b
}

let result = addClosure(3, 5)  // 返回 8
print(result)  // 输出：8
```

闭包可以作为参数传递给函数，这是闭包的常见用途。

**示例：使用闭包作为参数**

```swift
func performOperation(_ operation: (Int, Int) -> Int, on a: Int, and b: Int) {
    let result = operation(a, b)
    print("Result: \(result)")
}

performOperation({ (a, b) -> Int in
    return a + b
}, on: 3, and: 5)  // 输出：Result: 8
```

## 4. 闭包的简写语法

Swift 提供了闭包简写语法，可以通过上下文推断参数类型和返回类型，从而简化闭包的定义。可以逐步简化闭包的写法。

**省略参数类型和返回类型**

由于 Swift 可以通过上下文推断出参数类型和返回类型，可以省略这些部分。

```swift
performOperation({ a, b in
    return a + b
}, on: 3, and: 5)
```

**使用隐式返回**

如果闭包体只有一个表达式，那么可以省略 `return` 关键字。

```swift
performOperation({ a, b in a + b }, on: 3, and: 5)
```

**使用参数名称简写（$0, $1）**

Swift 允许使用自动生成的参数名称 `$0`, `$1`, 等，进一步简化闭包的书写。

```swift
performOperation({ $0 + $1 }, on: 3, and: 5)
```

**尾随闭包语法**

如果闭包是函数的最后一个参数，可以将闭包表达式放在函数调用的括号外，这种语法称为“尾随闭包”。

```swift
performOperation(on: 3, and: 5) { $0 + $1 }
```

## 5. 捕获值

闭包可以捕获并存储其上下文中的常量和变量。这意味着闭包可以“捕获”定义在其作用域中的值，并且可以在闭包体内进行使用，即使这些值的作用域已经不存在。

**1、示例：闭包捕获变量**

```swift
func makeIncrementer(incrementAmount: Int) -> () -> Int {
    var total = 0
    let incrementer: () -> Int = {
        total += incrementAmount
        return total
    }
    return incrementer
}

let incrementByTwo = makeIncrementer(incrementAmount: 2)
print(incrementByTwo())  // 输出：2
print(incrementByTwo())  // 输出：4
print(incrementByTwo())  // 输出：6
```

在这个例子中，`incrementByTwo` 闭包捕获了 `total` 和 `incrementAmount` 的值，即使 `makeIncrementer` 函数已经返回，`total` 变量依然可以在每次调用闭包时被修改。

#### 2、闭包捕获列表

闭包会对捕获的值保持强引用，可能导致**循环引用**问题。通过捕获列表可以控制闭包对捕获值的引用强度，防止内存泄漏。

```swift
class SomeClass {
    var x = 10
    func doSomething() {
        // 捕获 self，但使用 `[weak self]` 以避免强引用循环
        let closure = { [weak self] in
            print(self?.x ?? 0)
        }
        closure()
    }
}

let instance = SomeClass()
instance.doSomething()  // 输出：10
```

在这个例子中，`[weak self]` 可以防止闭包对 `self` 形成强引用，从而避免潜在的循环引用问题。



## 6、闭包类型

#### 1. 自动闭包 (`@autoclosure`)

`@autoclosure` 是一种将表达式自动封装为闭包的机制，常用于延迟求值。<mark style="color:red;">**自动闭包不接受参数**</mark>，当它被调用时会自动返回内部表达式的结果。

**示例：自动闭包**

```swift
func printIfTrue(_ condition: @autoclosure () -> Bool) {
    if condition() {
        print("It's true!")
    }
}

printIfTrue(3 > 1)  // 输出：It's true!
```

在这里，`3 > 1` 被自动封装成一个闭包，并在函数内部被调用。

#### 2、 非逃逸闭包

默认情况下，闭包是非逃逸的，也就是说，<mark style="color:red;">闭包是在函数返回之前就被执行</mark>。非逃逸闭包通常不需要显式声明，编译器可以优化其生命周期。

**示例：非逃逸闭包**

```swift
func someFunctionWithNonEscapingClosure(closure: () -> Void) {
    closure()  // 闭包在函数返回之前执行
}

someFunctionWithNonEscapingClosure {
    print("This is a non-escaping closure.")
}
```

#### 3、逃逸闭包 (`@escaping`)

默认情况下，闭包是在函数内立即执行的。如果需要将闭包传递给一个异步操作，并在函数返回后再执行，则闭包必须标记为 `@escaping`，即闭包“逃逸”出函数的作用域。

**示例：逃逸闭包**

```swift
var completionHandlers: [() -> Void] = []

func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}

someFunctionWithEscapingClosure {
    print("This is an escaping closure.")
}

completionHandlers[0]()  // 输出：This is an escaping closure.
```

在这个例子中，闭包被存储在 `completionHandlers` 数组中，并在函数返回后被调用，因此它是一个逃逸闭包。



闭包是 Swift 中强大而灵活的功能，支持简洁的语法和复杂的行为，例如捕获上下文变量、作为函数参数、返回值、逃逸闭包和自动闭包。通过灵活地使用闭包，开发者可以编写出简洁且易读的异步代码、回调机制等。
