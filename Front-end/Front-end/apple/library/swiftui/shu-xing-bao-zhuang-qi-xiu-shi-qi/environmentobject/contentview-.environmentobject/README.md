# ContentView().environmentObject

是的，这两者是配套使用的。

1. `ContentView().environmentObject(productsModel)`：这里的 `environmentObject(productsModel)` 是将一个 `ProductsModel` 的实例作为环境对象传递给视图树中的所有子视图。它通过 `environmentObject` 方法来共享数据，使得这个对象可以在子视图中被访问。
2. `@EnvironmentObject var productsModel: ProductsModel`：这里的 `@EnvironmentObject` 属性包装器用于声明这个视图依赖于某个环境对象，表示这个视图需要从父视图或视图树中获得一个类型为 `ProductsModel` 的共享实例。

这两者的关系是：你在父视图或某个视图中用 `.environmentObject()` 提供了一个对象实例，然后子视图通过 `@EnvironmentObject` 获取这个对象。这使得视图能够共享和依赖同一个模型数据。

总结：`.environmentObject(productsModel)` 是设置环境对象，`@EnvironmentObject` 是使用这个环境对象。

从父视图传递到子视图， 类似React中的一个好像叫做React.createContext()

