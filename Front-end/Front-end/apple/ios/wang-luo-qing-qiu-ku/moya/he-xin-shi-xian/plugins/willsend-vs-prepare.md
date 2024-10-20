# willSend vs prepare

`willSend` 和 `prepare` 在 Moya 中确实都有机会在请求发送之前进行操作，但它们的功能和应用场景有一定区别，它们并不是完全重复的。

#### 1. **`prepare`**：

* **时机**：`prepare` 在请求发送之前调用，并且是请求被**创建之后**，但**还未发送**时的最后一步。它的目的是允许开发者对**实际的 `URLRequest`** 进行修改。
* **作用**：你可以在 `prepare` 中修改请求的具体内容，比如设置请求头、参数、编码方式等。它直接修改的是 `URLRequest`，并且会返回一个新的或修改过的 `URLRequest`。
* **典型用途**：
  * 在请求头中添加认证信息，比如 `Authorization` token。
  * 修改请求的 URL、HTTP 方法、请求体等。

**示例**：

```swift
func prepare(_ request: URLRequest, target: TargetType) -> URLRequest {
    var request = request
    request.addValue("Bearer token", forHTTPHeaderField: "Authorization")
    return request
}
```

#### 2. **`willSend`**：

* **时机**：`willSend` 在请求**即将被发送**到网络之前调用。此时，`URLRequest` 已经完全准备好，并且不会再被修改。`willSend` 是请求即将发出的一个通知回调，无法再修改请求。
* **作用**：`willSend` 通常用于记录或观察请求的状态，比如打印日志、跟踪网络请求等。它不允许你再改变请求内容。
* **典型用途**：
  * 打印日志或调试信息。
  * 监控请求的状态，比如启动加载动画或计时器。

**示例**：

```swift
func willSend(_ request: RequestType, target: TargetType) {
    print("Sending request to: \(request.request?.url?.absoluteString ?? "")")
}
```

#### 主要区别

* **修改请求的能力**：
  * `prepare` 能够修改请求，它的返回值是一个可修改的 `URLRequest`，适合用来修改请求头、参数等内容。
  * `willSend` 仅仅是通知请求即将发送，它不能修改请求，只能用来监控或记录请求信息。
* **调用时机**：
  * `prepare` 在请求完全准备好但还未发送之前调用，它负责请求的最终调整。
  * `willSend` 是在请求即将发送到网络之前调用，适合用于记录或执行一些与请求内容无关的操作。

#### 总结

`prepare` 和 `willSend` 虽然都在请求发送前被调用，但它们的功能不同。`prepare` 是用于修改和调整请求，而 `willSend` 则是一个监控和记录的机会。通过这两者，Moya 提供了更细粒度的控制，以确保开发者能够灵活地定制网络请求的整个生命周期。
