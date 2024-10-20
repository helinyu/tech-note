# Response

在 Moya 中，`Response` 类是用于表示网络请求返回的数据，它封装了请求的结果，包括 HTTP 状态码、响应头、响应体等信息。通过 `Response` 对象，开发者可以轻松处理请求的结果，解析响应内容，处理错误等。

#### `Response` 的主要作用

Moya 的 `Response` 类主要是处理和管理网络请求的响应数据。它提供了访问 HTTP 请求结果的接口，并简化了对返回数据的处理，例如：将响应体解析成 JSON 或模型对象，提取状态码和头信息等。

#### `Response` 的核心属性

`Response` 包含了所有请求返回的关键信息，这些信息在处理 API 响应时非常有用：

1. **`statusCode`**：
   * HTTP 响应状态码，例如 `200` 表示请求成功，`404` 表示找不到资源等。你可以根据状态码决定如何处理响应。
   *   **示例**：

       ```swift
       let statusCode = response.statusCode
       if statusCode == 200 {
           print("Request succeeded!")
       }
       ```
2. **`data`**：
   * 响应体的二进制数据。这是服务器返回的实际数据，通常需要将其解析为 JSON 或其他格式来使用。
   *   **示例**：

       ```swift
       let responseData = response.data
       ```
3. **`response`**：
   * 原始的 `HTTPURLResponse` 对象，包含了所有与响应相关的底层信息，比如响应头、HTTP 版本等。
   *   **示例**：

       ```swift
       let headers = response.response?.allHeaderFields
       ```

#### `Response` 的方法

`Response` 提供了一些便捷的方法来帮助开发者处理和解析响应数据：

1. **`mapJSON()`**：
   * 将响应体数据转换为 JSON 格式，适用于返回 JSON 的 API 响应。
   *   **示例**：

       ```swift
       do {
           let json = try response.mapJSON()
           print(json)
       } catch {
           print("Failed to parse JSON")
       }
       ```
2. **`mapString()`**：
   * 将响应体数据转换为字符串格式，适用于返回文本或 HTML 内容的响应。
   *   **示例**：

       ```swift
       do {
           let stringResponse = try response.mapString()
           print(stringResponse)
       } catch {
           print("Failed to parse string")
       }
       ```
3. **`map<T: Decodable>(_ type: T.Type)`**：
   * 使用 `Codable` 将响应体数据解析为指定的模型对象，适合直接将 JSON 转换为 Swift 结构体或类。
   *   **示例**：

       ```swift
       struct User: Decodable {
           let id: Int
           let name: String
       }

       do {
           let user = try response.map(User.self)
           print(user.name)
       } catch {
           print("Failed to map response to User")
       }
       ```
4. **`filter(statusCode: Int)`**：
   * 通过状态码过滤响应，如果状态码不匹配，则抛出错误。常用于确保请求成功。
   *   **示例**：

       ```swift
       do {
           let filteredResponse = try response.filter(statusCode: 200)
           // 请求成功，继续处理响应数据
       } catch {
           print("Request failed with status code: \(response.statusCode)")
       }
       ```
5. **`filterSuccessfulStatusCodes()`**：
   * 自动过滤成功的状态码（200 到 299）。如果状态码不在这个范围内，会抛出错误。
   *   **示例**：

       ```swift
       do {
           let successResponse = try response.filterSuccessfulStatusCodes()
           // 请求成功
       } catch {
           print("Request failed")
       }
       ```

#### 典型的响应处理流程

当 Moya 请求返回一个 `Response` 对象后，通常你会对它进行解析，处理成功和失败的响应。

```swift
provider.request(.getUser(id: 123)) { result in
    switch result {
    case let .success(response):
        do {
            // 确保状态码为 200-299
            let filteredResponse = try response.filterSuccessfulStatusCodes()
            
            // 将响应体解析为 JSON
            let json = try filteredResponse.mapJSON()
            print("Parsed JSON: \(json)")
            
            // 或者直接映射为模型对象
            let user = try filteredResponse.map(User.self)
            print("User name: \(user.name)")
        } catch {
            print("Error parsing response: \(error)")
        }
        
    case let .failure(error):
        // 处理请求失败
        print("Request failed: \(error)")
    }
}
```

#### 小结

Moya 的 `Response` 类简化了处理网络请求响应的过程，提供了对 HTTP 状态码、响应数据、响应头等的便捷访问方式。通过提供丰富的解析方法，如 `mapJSON()`、`mapString()` 和 `map`，开发者可以轻松将服务器返回的数据转换为可用的格式或模型，极大地提高了开发效率。
