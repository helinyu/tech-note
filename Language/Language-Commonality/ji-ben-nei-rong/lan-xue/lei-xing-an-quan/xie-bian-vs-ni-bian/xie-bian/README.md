# 协变

编程语言中的 <mark style="color:red;">**协变**</mark>**（covariance）** **概念源于类型系统的多态性规则，主要用于处理类型参数，使代码在类型检查时更灵活。**协变允许将 **子类型（subtype）** 作为 **父类型（supertype）** 的替代类型，主要出现在泛型、集合和函数返回类型中。简而言之，协变让子类替换父类成为可能，而不破坏类型安全。

#### 协变的用途

<mark style="color:red;">协变常用于需要传递、返回或赋值包含更具体类型的集合或对象时</mark>。在这些场景中，协变提供了更大的灵活性，使代码可以在不改变类型的情况下兼容更多对象类型。

#### 编程语言中的协变实现

以下是一些编程语言中如何实现和使用协变的示例。

**1. Objective-C**

Objective-C 的 `__covariant` 修饰符用于泛型类型参数，允许子类型赋值给父类型的变量。通过此修饰符，开发者可以定义支持协变的泛型集合。

```objective-c
@interface MyContainer<__covariant ObjectType> : NSObject
@property (nonatomic, strong) ObjectType containedObject;
@end
```

使用时可以将 `MyContainer<NSString *>` 赋值给 `MyContainer<id>`，因为 `NSString` 是 `id` 的子类。

**2. Swift**

在 Swift 中，数组等集合类型天然支持协变。例如，如果 `Cat` 是 `Animal` 的子类，则 `Array<Cat>` 可以赋值给 `Array<Animal>` 类型的变量。

```swift
class Animal {}
class Cat: Animal {}

let cats: [Cat] = [Cat()]
let animals: [Animal] = cats // 协变
```

**3. Java**

Java 使用通配符 `? extends` 来支持协变。例如，`List<? extends Animal>` 类型的变量可以引用 `List<Dog>` 或 `List<Cat>` 类型的对象。

```java
class Animal {}
class Dog extends Animal {}

List<Dog> dogs = new ArrayList<>();
List<? extends Animal> animals = dogs; // 协变
```

**4. C#**

C# 中的协变使用 `out` 关键字来修饰接口或委托的类型参数。`out` 关键字使类型参数协变，表示该类型参数可以是派生类类型的集合。

```csharp
public interface IEnumerable<out T> { }

public class Animal { }
public class Cat : Animal { }

IEnumerable<Cat> cats = new List<Cat>();
IEnumerable<Animal> animals = cats; // 协变
```

**5. Kotlin**

Kotlin 使用 `out` 关键字来表示协变。标记为 `out` 的泛型类型参数可以用在返回类型中，但不能用作参数类型。

```kotlin
open class Animal
class Cat : Animal()

val cats: List<Cat> = listOf()
val animals: List<Animal> = cats // 协变
```

#### 协变的关键特性

* **只读场景**：协变通常应用于只读集合或接口，因为协变限制了向集合中添加元素的能力（只能从中读取），保证类型安全。
* **灵活性**：协变允许更灵活地使用集合、接口等泛型数据结构，尤其在多态性较强的代码中。
* **函数返回类型**：在函数返回类型中使用协变可以提供更具体的类型，符合多态性原则。

#### 总结

协变是面向对象编程中处理类型继承的重要特性，解决了父子类型在泛型和集合中的兼容问题。在 Objective-C、Swift、Java、C#、Kotlin 等语言中，协变提高了代码的复用性和灵活性，使得多态操作更加自然。
