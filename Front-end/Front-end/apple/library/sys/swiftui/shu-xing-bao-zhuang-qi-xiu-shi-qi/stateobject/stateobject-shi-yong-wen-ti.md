# @stateObject使用问题

[源码文件](https://github.com/VCBSstudio/ScreenCut/blob/main/ScreenCut/ScreenCut/BottomView/EditCutBottomView.swift)

@StateObject private var actionItem = EditActionShareModel.shared 这里为什么会显示错误？ actionItem.actionType = .download

这样使用会出现提示：&#x20;

&#x20;Accessing StateObject's object without being installed on a View. This will create a new instance each time.



这个错误的原因是因为`@StateObject`应该用于**在视图中管理一个新的实例**，而在你的代码中，你试图将一个**单例对象**（`EditActionShareModel.shared`）赋值给`@StateObject`，这在SwiftUI中不符合`@StateObject`的设计原则。

在SwiftUI中，`@StateObject`用于在视图的生命周期内**创建并管理新的对象实例**。因此，它需要在`View`的初始化过程中直接赋值为一个新的实例，而不能直接用一个现有的共享实例或单例对象来初始化，否则SwiftUI会误认为这是一个新的对象，每次访问时会导致重新初始化，并且显示警告。

#### 如何修复

如果`EditActionShareModel`是一个单例对象（即通过`shared`静态属性来共享一个实例），在SwiftUI中应该使用`@ObservedObject`或`@EnvironmentObject`而不是`@StateObject`，因为你不希望SwiftUI重新管理和创建它。

```swift
// 使用@ObservedObject而不是@StateObject
@ObservedObject private var actionItem = EditActionShareModel.shared
```

#### 解释

* `@ObservedObject`用于**引用**外部传入的对象（如单例对象或父视图传入的模型），而不是创建和管理它。
* `@StateObject`应该用于**在视图内部创建的新对象**，并且让SwiftUI管理它的生命周期。

通过将`@StateObject`改为`@ObservedObject`，你可以避免这个错误，并且每次访问`EditActionShareModel.shared`时都能访问到同一个实例。

可以看上面的对比。

