# 本地服务的网络请求设置

在Xcode中配置HTTP请求需要进行以下几个步骤：

1.  **修改`Info.plist`文件**：

    <figure><img src="../../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>



    * `Allows Local Networking`是一个布尔值，用于控制是否允许本地网络访问。
    * `Local Networking Exception Usage`是一个描述性字符串，说明应用为什么需要这个权限。
2.  **使用`URLSession`进行HTTP请求**：

    * 在你的代码中，你可以使用`URLSession`来发送HTTP请求。例如：

    ```swift
    import Foundation

    let url = URL(string: "http://example.com")!
    let task = URLSession.shared.dataTask(with: url) { data, response, error in
        if let error = error {
            print("Error: \(error)")
            return
        }
        if let data = data {
            let responseString = String(data: data, encoding: .utf8)
            print("Response: \(responseString ?? "")")
        }
    }
    task.resume()
    ```
3. **测试和调试**：
   * 运行你的应用程序，确保它能够成功发出HTTP请求并处理响应。
