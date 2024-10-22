# KVC的赋值和取值过程是怎样的？原理是什么？

在 Objective-C 中，**KVC（Key-Value Coding）** 是一种间接访问对象属性的机制。通过 `KVC`，你可以在运行时通过字符串来获取或设置对象的属性值，而不需要直接调用属性的 getter 和 setter 方法。KVC 使用了动态消息机制和反射来完成这个任务。

#### KVC 赋值过程 (`setValue:forKey:`)：

当你使用 `KVC` 给对象的属性赋值时，系统会按以下顺序查找并设置值：

**1. 查找是否有对应的 Setter 方法：**

* KVC 会首先寻找与 key 对应的 **setter 方法**。假设 key 是 `name`，那么它会寻找 `setName:` 方法。
* 如果找到了这个 setter 方法，它会直接调用该方法来设置属性值。

**2. 如果没有找到 Setter 方法，KVC 会查找实例变量（iVar）：**

* accessInstanceVariablesDirectly == YES， 默认，就会访问变量
* 如果对象没有提供 `set<Key>:` 方法，KVC 会直接访问对象的实例变量，寻找命名为 `_key`、`_isKey`、`key` 或 `isKey` 的变量（按这个顺序查找）。
* 一旦找到匹配的实例变量，KVC 会直接赋值。
* 如果变量是只读的（没有 setter 方法但有实例变量），KVC 仍然可以通过这种方式直接赋值。

**3. `setValue:forUndefinedKey:`：**

* 如果上面的两步都没有找到 setter 或实例变量，KVC 会调用 `setValue:forUndefinedKey:` 方法。
* 这个方法默认会抛出异常，但你可以通过重写该方法来处理未知的 key。

**4. `setNilValueForKey:`：**

* 如果试图将 `nil` 设置给一个非对象类型（如 `int`、`float` 等）的属性，KVC 会调用 `setNilValueForKey:` 方法。默认情况下，这个方法会抛出异常，你可以通过重写它来处理 `nil` 值。

#### KVC 取值过程 (`valueForKey:`)：

当你使用 `KVC` 获取对象的属性值时，系统会按以下顺序查找：

**1. 查找 Getter 方法：**

* KVC 首先会查找对应的 getter 方法。假设 key 是 `name`，它会寻找 `getName`、`name` 或 `isName` 方法。
* 如果找到了匹配的 getter 方法，KVC 会调用该方法来获取属性值。

**2. 查找实例变量：**

* accessInstanceVariablesDirectly == YES， 默认，就会访问变量
* 如果没有找到 getter 方法，KVC 会直接访问实例变量，寻找命名为 `_key`、`_isKey`、`key` 或 `isKey` 的变量。
* 找到后，它会直接返回这个实例变量的值。

**3. `valueForUndefinedKey:`：**

* 如果上面的两步都没有找到 getter 或实例变量，KVC 会调用 `valueForUndefinedKey:` 方法。
* 这个方法默认会抛出异常，但可以通过重写它来返回一个默认值。

**4. 访问集合类型：**

* 如果属性是集合类型（如数组、字典等），KVC 支持对集合的访问。例如，`valueForKeyPath:` 可以通过路径访问集合中的元素或嵌套属性。

#### KVC 的实现原理：

KVC 的实现依赖于 **Objective-C 的运行时机制**（Runtime），特别是以下几个特性：

* **动态方法调用**：KVC 可以通过运行时动态查找属性的 getter 和 setter 方法，并在运行时调用它们。
* **访问实例变量**：在找不到 setter/getter 方法时，KVC 直接通过 `runtime` 访问对象的实例变量。这种直接访问是通过 Objective-C 的反射机制实现的。
* **消息传递**：当使用 `setValue:forKey:` 或 `valueForKey:` 时，实际上是向对象发送一条消息，类似于 Objective-C 的动态消息机制。

#### KVC 使用的 Key Path：

除了使用单一的 key，KVC 还支持 **Key Path**，即通过路径访问嵌套对象的属性。例如：

```objc
NSString *cityName = [person valueForKeyPath:@"address.city"];
```

在这个例子中，KVC 会依次访问 `person` 对象的 `address` 属性，再访问 `address` 对象的 `city` 属性。

#### 总结：

* **赋值过程**：优先查找 setter 方法，找不到则直接访问实例变量，最终可能调用 `setValue:forUndefinedKey:`。
* **取值过程**：优先查找 getter 方法，找不到则访问实例变量，最终可能调用 `valueForUndefinedKey:`。
* **实现原理**：KVC 借助 Objective-C 的运行时机制，通过动态方法查找和实例变量访问，提供了灵活的间接属性访问方式。



<figure><img src="../../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>
