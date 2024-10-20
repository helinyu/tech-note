# TargetType

定义了一个名为 `TargetType` 的协议，用于规范 `MoyaProvider` 所需的目标类型。具体功能如下：

1. **协议定义**：
   * `baseURL`: 目标的基URL。
   * `path`: 附加到 `baseURL` 的路径。
   * `method`: 请求使用的HTTP方法。
   * `sampleData`: 用于测试的存根数据，默认为 `Data()`。
   * `task`: 要执行的HTTP任务类型。
   * `validationType`: 请求验证类型，默认为 `.none`。
   * `headers`: 请求头。
2. **默认实现**：
   * `validationType` 默认为 `.none`。
   * `sampleData` 默认为 `Data()`。
