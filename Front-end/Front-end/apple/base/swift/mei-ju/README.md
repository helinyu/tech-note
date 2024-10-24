# 枚举

在 Swift 中，枚举（`enum`）是一种自定义数据类型，允许定义一组相关的值。枚举可以具有附加的值（关联值）和方法，非常灵活和强大。以下是 Swift 中枚举的一些基本概念和示例：

#### 基本语法

```swift
enum Direction {
    case north
    case south
    case east
    case west
}
```

#### 使用枚举

你可以通过以下方式使用枚举：

```swift
let currentDirection = Direction.north

switch currentDirection {
case .north:
    print("Heading North")
case .south:
    print("Heading South")
case .east:
    print("Heading East")
case .west:
    print("Heading West")
}
```

#### 关联值

枚举可以有关联值，允许存储额外的信息：

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

var productBarcode = Barcode.upc(123, 456, 789, 0)

switch productBarcode {
case .upc(let number1, let number2, let number3, let number4):
    print("UPC: \(number1) \(number2) \(number3) \(number4)")
case .qrCode(let code):
    print("QR Code: \(code)")
}
```

#### 原始值

枚举也可以定义原始值，所有的枚举成员可以具有相同类型的原始值：

```swift
enum Planet: Int {
    case mercury = 1
    case venus
    case earth
    case mars
}

let earthOrder = Planet.earth.rawValue  // 3
```

#### 递归枚举

枚举也可以是递归的，这意味着它可以包含自身的实例：

```swift
enum ArithmeticExpression {
    case number(Int)
    indirect case addition(ArithmeticExpression, ArithmeticExpression)
    indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}

let expression = ArithmeticExpression.addition(
    .number(2),
    .multiplication(.number(3), .number(4))
)
```

#### 总结

1、基本的列举

2、关联至

3、递归枚举

