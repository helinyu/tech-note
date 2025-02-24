# 主要内容

`Response`的类，用于表示网络请求的响应。主要功能包括：

1. **属性**：
   * `statusCode`: 响应的状态码。
   * `data`: 响应的数据。
   * `request`: 原始的URLRequest。
   * `response`: HTTPURLResponse对象。
2. **初始化方法**：
   * `init(statusCode:data:request:response:)`: 初始化`Response`对象。
3. **描述方法**：
   * `description`: 返回响应的文本描述。
   * `debugDescription`: 返回适合调试的文本描述。
4. **过滤方法**：
   * `filter(statusCodes:)`: 检查状态码是否在指定范围内，不在范围内则抛出异常。
   * `filter(statusCode:)`: 检查状态码是否为指定值，不是则抛出异常。
   * `filterSuccessfulStatusCodes()`: 检查状态码是否在200-299范围内，不在范围内则抛出异常。
   * `filterSuccessfulStatusAndRedirectCodes()`: 检查状态码是否在200-399范围内，不在范围内则抛出异常。
5. **映射方法**：
   * `mapImage()`: 将数据映射为图像。
   * `mapJSON(failsOnEmptyData:)`: 将数据映射为JSON对象。
   * `mapString(atKeyPath:)`: 将数据映射为字符串，支持指定键路径。
   * `map(_:atKeyPath:using:failsOnEmptyData:)`: 将数据映射为可解码对象，支持指定键路径和解码器。

map 方法流程：

<figure><img src="../../../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

