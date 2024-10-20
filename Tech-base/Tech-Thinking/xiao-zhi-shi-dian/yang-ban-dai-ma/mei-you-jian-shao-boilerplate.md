# 没有减少boilerplate

如果没有使用 Moya，上述代码需要更多的手动配置和重复代码。以下是没有 Moya 的版本，展示了如何手动处理请求和响应：

#### 1. 定义 API 请求

你需要手动编写请求的 URL 和参数。

<pre class="language-swift"><code class="lang-swift">import Alamofire

<strong>func getUser(id: Int, completion: @escaping (Result&#x3C;User, Error>) -> Void) {
</strong>    let url = "https://api.example.com/user/\(id)"
    
    AF.request(url).responseJSON { response in
        switch response.result {
        case .success(let value):
            do {
                let data = try JSONSerialization.data(withJSONObject: value)
                let user = try JSONDecoder().decode(User.self, from: data)
                completion(.success(user))
            } catch {
                completion(.failure(error))
            }
        case .failure(let error):
            completion(.failure(error))
        }
    }
}

func createUser(name: String, completion: @escaping (Result&#x3C;User, Error>) -> Void) {
    let url = "https://api.example.com/user"
    let parameters: [String: Any] = ["name": name]

    AF.request(url, method: .post, parameters: parameters, encoding: JSONEncoding.default).responseJSON { response in
        switch response.result {
        case .success(let value):
            do {
                let data = try JSONSerialization.data(withJSONObject: value)
                let user = try JSONDecoder().decode(User.self, from: data)
                completion(.success(user))
            } catch {
                completion(.failure(error))
            }
        case .failure(let error):
            completion(.failure(error))
        }
    }
}
</code></pre>

#### 2. 错误处理

错误处理也需要重复代码，且每次都需要手动处理响应结果。

```swift
provider.request(.getUser(id: 1)) { result in
    switch result {
    case .success(let response):
        // 处理逻辑...
    case .failure(let error):
        // 处理逻辑...
    }
}
```

#### 总结

没有 Moya，你将不得不重复许多配置和响应处理的代码，导致代码可读性降低和维护成本增加。Moya 的引入使得网络请求更具结构化和模块化，从而减少了这些重复的 boilerplate 代码。
