# 通过泛型来解析数据类型

在 Swift 中，当你尝试在子类中重写一个属性时，新属性的类型必须与父类中的原始属性类型兼容。在你提供的代码中，WADataBaseResponse 类定义了一个名为 data 的属性，其类型为 Any?。而在 WAUserBannerlistResponse 子类中，你尝试用更具体化的类型 \[WAUserBannerModel]? 来重写它。Swift 不允许直接改变被重写的属性的类型，即使新的类型是旧类型的子类型，因为这会违反里氏替换原则（Liskov Substitution Principle），即子类应当可以替换父类而不影响程序的正确性。为了实现你的需求，你可以采取以下几种方法之一：

1. \*\*泛型\*\*：使父类变为泛型类，并指定 data 属性的类型参数。
2. \*\*类型转换\*\*：保持 data 属性为 Any? 类型，在需要时使用类型转换来获取具体的类型。
3. \*\*添加新属性\*\*：在子类中添加一个新的属性，用于存储特定类型的值，同时保留继承自父类的 data 属性。

下面是使用泛型的方式实现的例子：

```
class WADataBaseResponse<T>: WABaseObservableHandyJson {
    var code: Int
    var msg: String
    var data: T?
    var traceId: String
    var timestamp: String
    
    required init() {
        code = 0
        msg = ""
        data = nil
        traceId = ""
        timestamp = ""
    }
}

class WAUserBannerlistResponse: WADataBaseResponse<[WAUserBannerModel]> {
    // 这里不需要重写 `data` 属性，因为它已经通过泛型指定了类型
}
```



在这个例子中，我们通过将 WADataBaseResponse 定义为泛型类，并将 data 属性的类型设置为泛型参数 T，从而解决了问题。这样，WAUserBannerlistResponse 就可以指定 data 的确切类型了。\


#### 一个网络请求的示例代码：

```

func loadHotBannerList() {
        mockUserProvider.request(.userBannerList(category: 4)) { result in
            if self.hotDataResetRefreshing {
                self.hotDataResetRefreshing = false
            }
            switch result {
            case .success(let response):
                do {
                    if let jsonDict = try JSONSerialization.jsonObject(with: response.data, options: []) as? [String: Any] ,let responseData = WADataBaseResponse<[WAUserBannerModel]>.deserialize(
                        from: jsonDict
                    ) {
                        if responseData.code == 200 {
                            self.bannerList = responseData.data ?? []
                        }
                        else {
                            // 这个地方到时候统一处理
                        }
                    }
                    else {
                        print("errorro : \(response.data)")
                    }
                }
                catch {
                    print("decode error : \(error.localizedDescription)")
                }
            case .failure(let error):
                print("request failed with error : \(error.localizedDescription)")
            }
        }
    }
```

主要是这里： WADataBaseResponse<\[WAUserBannerModel]>.deserialize  ，主要我们传入我们想要的数据类型就可以了，因为data可能是数组，也能是字典，传上对应的模型，就可以解决类型判断的问题了。

