# 类比React

在 React 中，`@EnvironmentObject` 的概念可以对应于 **Context API**。React 的 Context API 允许在组件树中共享状态，类似于 SwiftUI 中的 `@EnvironmentObject`。

React 的 Context API 的用法可以通过以下几个步骤实现：

1.  **创建 Context：** 使用 `React.createContext()` 创建一个 Context 对象。

    ```js
    const ProductsContext = React.createContext();
    ```
2.  **提供 Context：** 在应用的某个父组件中，使用 `ProductsContext.Provider` 提供共享的数据。

    ```js
    function App() {
      const productsModel = { /* 一些共享的数据 */ };
      
      return (
        <ProductsContext.Provider value={productsModel}>
          <ContentView />
        </ProductsContext.Provider>
      );
    }
    ```
3.  **消费 Context：** 在子组件中，可以使用 `useContext` 钩子来访问 Context 中的值，相当于 SwiftUI 中的 `@EnvironmentObject`。

    ```js
    import { useContext } from 'react';

    function ContentView() {
      const productsModel = useContext(ProductsContext);
      
      return (
        <div>{/* 使用 productsModel */}</div>
      );
    }
    ```

React 的 Context API 与 SwiftUI 的 `@EnvironmentObject` 类似，都用于在组件树中共享状态，避免手动逐级传递 props。

