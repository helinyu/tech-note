# 简单工厂、工厂方法、抽象工厂

**简单工厂**： 简单的switch..case 或者if 来分类创建对象  —— 具体哪一个（1个）

**工厂方法**： 基于简单工厂， 让子类来创建对象 —— 具体哪一个（1个）

**抽象工厂**： 创建一系列的对象 —— 一系列对象（多个）



它们的共同目的是通**过封装对象创建的过程，减少客户端代码对具体类的依赖**，从而提高系统的灵活性和可扩展性。尽管它们的目标类似，但它们的<mark style="color:red;">使用场景和实现方式有所不同</mark>。

#### 1. **简单工厂设计模式（Simple Factory Pattern）**

简单工厂模式并不是正式的设计模式，而是常见的创建模式之一。它通过一个工厂类来根据参数创建不同的对象。

**结构：**

* **工厂类**：一个工厂类，它根据不同的条件创建和返回不同类型的对象。
* **客户端**：客户端通过工厂类请求对象，而无需了解具体的类名或实例化过程。

**特点：**

* **单一工厂类**：所有对象创建逻辑集中在一个工厂类中。
* **无法扩展**：当需要添加新的产品类时，必须修改工厂类，不符合开放封闭原则（OCP）。

**示例：**

```swift
class Animal {
    func speak() {}
}

class Dog: Animal {
    override func speak() {
        print("Woof")
    }
}

class Cat: Animal {
    override func speak() {
        print("Meow")
    }
}

class AnimalFactory {
    static func createAnimal(type: String) -> Animal? {
        switch type {
        case "dog":
            return Dog()
        case "cat":
            return Cat()
        default:
            return nil
        }
    }
}

// 使用
let dog = AnimalFactory.createAnimal(type: "dog")
dog?.speak()  // 输出: Woof
```

**适用场景：**

* 当对象创建非常简单且不需要进行复杂的实例化时使用。
* 客户端可以通过工厂获取不同类型的对象，但不需要了解这些对象的具体实现。

#### 2. **工厂方法设计模式（Factory Method Pattern）**

工厂方法模式是 **简单工厂模式** 的一种扩展，它通过定义一个接口来创建对象，但由子类决定实例化哪个类。每个子类实现这个工厂方法来创建具体对象。

**结构：**

* **抽象工厂类**：定义一个创建产品的抽象方法，子类实现该方法来生产具体产品。
* **具体工厂类**：实现抽象工厂类，创建具体产品。
* **产品接口**：定义一组产品的方法（接口）。
* **具体产品类**：实现产品接口，定义具体产品的功能。

**特点：**

* **封装对象创建**：客户端无需知道具体产品类，通过工厂方法得到产品对象。
* **可扩展性强**：如果需要新增产品，只需要添加新的具体工厂类，而不需要修改原有代码（符合开放封闭原则）。

**示例：**

```swift
protocol Animal {
    func speak()
}

class Dog: Animal {
    func speak() {
        print("Woof")
    }
}

class Cat: Animal {
    func speak() {
        print("Meow")
    }
}

protocol AnimalFactory {
    func createAnimal() -> Animal
}

class DogFactory: AnimalFactory {
    func createAnimal() -> Animal {
        return Dog()
    }
}

class CatFactory: AnimalFactory {
    func createAnimal() -> Animal {
        return Cat()
    }
}

// 使用
let dogFactory: AnimalFactory = DogFactory()
let dog = dogFactory.createAnimal()
dog.speak()  // 输出: Woof
```

**适用场景：**

* 当需要创建的对象属于同一产品族，但具体产品可能在不同子类中实现时。
* 客户端通过具体工厂方法来创建对象，不需要关心产品的具体类。

#### 3. **抽象工厂设计模式（Abstract Factory Pattern）**

抽象工厂模式是在 **工厂方法模式** 的基础上进一步扩展的，它提供了一个创建一系列相关或依赖对象的接口，而无需指定具体类。通过抽象工厂类，客户端可以创建一组相关产品，而这些产品属于<mark style="color:red;">同一产品族</mark>。

**结构：**

* **抽象工厂类**：定义创建一系列产品的方法（每种产品对应一个方法）。
* **具体工厂类**：实现抽象工厂类，创建具体的产品。
* **抽象产品类**：定义一组产品的接口。
* **具体产品类**：实现产品接口，定义具体产品的功能。
* **客户端**：通过抽象工厂类获取产品，不需要关心具体实现。

**特点：**

* **产品族**：客户端可以选择创建一系列相关的产品（而非单一产品）。
* **扩展性强**：若需要添加新的产品族，只需添加新的具体工厂类，符合开放封闭原则。
* **可维护性强**：工厂类和产品类分离，易于管理和维护。

**示例：**

```swift
protocol Button {
    func render()
}

protocol ScrollBar {
    func render()
}

class MacButton: Button {
    func render() {
        print("Mac Button")
    }
}

class MacScrollBar: ScrollBar {
    func render() {
        print("Mac Scroll Bar")
    }
}

class WindowsButton: Button {
    func render() {
        print("Windows Button")
    }
}

class WindowsScrollBar: ScrollBar {
    func render() {
        print("Windows Scroll Bar")
    }
}

protocol GUIFactory {
    func createButton() -> Button
    func createScrollBar() -> ScrollBar
}

class MacFactory: GUIFactory {
    func createButton() -> Button {
        return MacButton()
    }
    
    func createScrollBar() -> ScrollBar {
        return MacScrollBar()
    }
}

class WindowsFactory: GUIFactory {
    func createButton() -> Button {
        return WindowsButton()
    }
    
    func createScrollBar() -> ScrollBar {
        return WindowsScrollBar()
    }
}

// 使用
let macFactory: GUIFactory = MacFactory()
let button = macFactory.createButton()
button.render()  // 输出: Mac Button
```

**适用场景：**

* 当系统需要创建一系列相关的产品对象时，并且这些对象都属于同一产品族。
* 系统需要独立于产品的创建、组合和表示。

#### 对比总结

<table><thead><tr><th width="133">特性</th><th>简单工厂模式（Simple Factory）</th><th>工厂方法模式（Factory Method）</th><th>抽象工厂模式（Abstract Factory）</th></tr></thead><tbody><tr><td><strong>目的</strong></td><td>封装对象创建过程，简化客户端的创建逻辑</td><td>允许子类决定实例化哪个具体类</td><td>创建一系列相关对象的接口</td></tr><tr><td><strong>客户端</strong></td><td>依赖于工厂类来创建具体的产品类</td><td>依赖于工厂接口，通过具体工厂类来创建</td><td>依赖于抽象工厂接口，创建一系列相关产品</td></tr><tr><td><strong>产品数量</strong></td><td>只能创建一种产品类型</td><td>创建单个产品类型，但可以有多个产品的子类</td><td>创建多个相关的产品（通常一对一）</td></tr><tr><td><strong>扩展性</strong></td><td>不太灵活，需要修改工厂类才能增加新产品</td><td>具有较好的扩展性，添加新产品只需新增子工厂</td><td>扩展性最强，可以轻松添加新的<mark style="color:red;">产品族</mark></td></tr><tr><td><strong>使用场景</strong></td><td>对象创建比较简单，或者客户端只需创建单一对象</td><td>客户端通过工厂方法来决定具体产品创建</td><td>创建相关产品族，且不希望客户端关心具体实现</td></tr></tbody></table>

#### 总结

* **简单工厂模式**：适用于需要通过简单的条件判断来创建少量不同类型对象的场景，通常不适合扩展。
* **工厂方法模式**：适用于需要创建不同产品的场景，但产品间有较强的继承关系，子类可以决定具体的产品。
* **抽象工厂模式**：适用于需要创建一系列相关产品（产品族）的场景，通过抽象工厂来管理多个产品的创建，具有较强的扩展性。

