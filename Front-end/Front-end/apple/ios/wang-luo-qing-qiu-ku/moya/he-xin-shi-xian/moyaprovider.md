# MoyaProvider

<figure><img src="../../../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>



Swift代码定义了网络请求库Moya的核心组件，包括请求完成闭包、进度更新闭包、进度响应结构体、提供者协议和提供者类。主要功能如下：

1. **闭包定义**：
   * `Completion`：请求完成时调用的闭包，参数为请求结果。
   * `ProgressBlock`：请求进度变化时调用的闭包，参数为进度响应。
2. **进度响应结构体**：
   * `ProgressResponse`：包含请求的响应和进度对象，提供了计算进度和判断请求是否完成的方法。
3. **提供者协议**：
   * `MoyaProviderType`：定义了最小接口，用于发起请求并返回可取消的令牌。
4. **提供者类**：
   * `MoyaProvider`：实现了`MoyaProviderType`协议，负责管理请求的生命周期，包括请求的创建、发送、取消和插件管理。
   * 提供了初始化方法、请求方法和存根请求方法。
5. **存根行为枚举**：
   * `StubBehavior`：定义了请求存根的行为，包括不存根、立即存根和延迟存根。
6. **公共扩展方法**：
   * `MoyaProvider`的扩展方法提供了常见的存根行为闭包。
7. **响应转换函数**：
   * `convertResponseToResult`：将`URLRequest`的结果转换为`Result<Moya.Response, MoyaError>`。

\
