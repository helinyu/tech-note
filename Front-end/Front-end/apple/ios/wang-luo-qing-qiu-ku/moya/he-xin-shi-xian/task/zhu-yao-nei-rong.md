# 主要内容

在 Moya 中，`Task` 是一个非常重要的枚举类型，用来定义一个 API 请求中实际的任务内容。具体来说，<mark style="color:red;">`Task`</mark> <mark style="color:red;"></mark><mark style="color:red;">指定了网络请求发送时携带的参数类型和参数的编码方式</mark>。它是构建 HTTP 请求的关键部分，用于指定请求中需要传递的数据或文件等内容。

#### `Task` 的主要作用

`Task` 的作用是在 Moya 中定义每个 API 请求的负载，告诉网络请求需要发送什么类型的数据，以及如何编码这些数据。无论是简单的 GET 请求、带有参数的 POST 请求，还是上传文件、多部分表单，`Task` 都能够满足需求。

#### `Task` 的常用类型

`Task` 枚举有多种类型，涵盖了不同形式的 HTTP 请求需求：

1. **`requestPlain`**：
   * 发送一个没有任何参数的请求，通常用于 GET 请求或不需要请求体的请求。
   *   **示例**：

       ```swift
       var task: Task {
           return .requestPlain
       }
       ```
2. **`requestData(Data)`**：
   * 直接发送一段二进制数据，适用于需要直接发送序列化后的数据的请求。
   *   **示例**：

       ```swift
       var task: Task {
           let data = "example data".data(using: .utf8)!
           return .requestData(data)
       }
       ```
3. **`requestJSONEncodable(Encodable)`**：
   * 将 `Encodable` 对象自动转换为 JSON 格式，并作为请求体发送。这在处理复杂的 JSON 请求时非常方便。
   *   **示例**：

       ```swift
       struct User: Encodable {
           let id: Int
           let name: String
       }

       var task: Task {
           let user = User(id: 1, name: "John")
           return .requestJSONEncodable(user)
       }
       ```
4. **`requestParameters([String: Any], ParameterEncoding)`**：
   * 发送带有参数的请求，参数可以是字典，且可以指定编码方式（如 URL 编码、JSON 编码等）。这是一种非常常见的请求类型，适用于 POST、PUT 等请求。
   *   **示例**：

       ```swift
       var task: Task {
           return .requestParameters(parameters: ["id": 123, "name": "John"], encoding: URLEncoding.default)
       }
       ```
5. **`requestCompositeData(bodyData: Data, urlParameters: [String: Any])`**：
   * 允许同时发送 URL 参数和请求体数据。URL 参数会被附加到请求的 URL 上，而请求体数据会作为请求的主体。
   *   **示例**：

       ```swift
       var task: Task {
           let bodyData = "example data".data(using: .utf8)!
           return .requestCompositeData(bodyData: bodyData, urlParameters: ["key": "value"])
       }
       ```
6. **`requestCompositeParameters(bodyParameters: [String: Any], bodyEncoding: ParameterEncoding, urlParameters: [String: Any])`**：
   * 同时发送请求体参数和 URL 参数，允许为请求体参数指定编码方式。这种方式更灵活，适合复杂的 API 调用。
   *   **示例**：

       ```swift
       var task: Task {
           return .requestCompositeParameters(bodyParameters: ["name": "John"], bodyEncoding: JSONEncoding.default, urlParameters: ["id": 123])
       }
       ```
7. **`uploadFile(URL)`**：
   * 上传文件，文件以 URL 的形式传递。
   *   **示例**：

       ```swift
       var task: Task {
           let fileURL = URL(fileURLWithPath: "path/to/file")
           return .uploadFile(fileURL)
       }
       ```
8. **`uploadMultipart([MultipartFormData])`**：
   * 上传多部分表单数据，适合文件上传和表单提交的场景。每个 `MultipartFormData` 表示表单中的一个字段或文件。
   *   **示例**：

       ```swift
       var task: Task {
           let multipartData = MultipartFormData(provider: .file(fileURL), name: "file")
           return .uploadMultipart([multipartData])
       }
       ```
9. **`downloadDestination(DownloadDestination)`**：
   * 指定下载任务和下载文件的保存位置。`DownloadDestination` 定义了如何处理下载的文件。
   *   **示例**：

       ```swift
       var task: Task {
           let destination: DownloadDestination = { _, _ in
               let fileURL = URL(fileURLWithPath: "path/to/file")
               return (fileURL, [.removePreviousFile, .createIntermediateDirectories])
           }
           return .downloadDestination(destination)
       }
       ```
10. **`downloadParameters([String: Any], ParameterEncoding, DownloadDestination)`**：
    * 允许发送带有参数的下载请求，并指定下载文件的保存位置。
    *   **示例**：

        ```swift
        var task: Task {
            let destination: DownloadDestination = { _, _ in
                let fileURL = URL(fileURLWithPath: "path/to/file")
                return (fileURL, [.removePreviousFile, .createIntermediateDirectories])
            }
            return .downloadParameters(["id": 123], URLEncoding.default, destination)
        }
        ```

#### 小结

在 Moya 中，`Task` 的作用是为每个 API 请求指定请求的内容和数据结构。它让你能够灵活定义请求参数、请求体以及如何编码数据，从而支持从简单的 GET 请求到复杂的文件上传和下载。通过使用不同的 `Task` 类型，Moya 可以轻松处理各种 HTTP 请求场景。
