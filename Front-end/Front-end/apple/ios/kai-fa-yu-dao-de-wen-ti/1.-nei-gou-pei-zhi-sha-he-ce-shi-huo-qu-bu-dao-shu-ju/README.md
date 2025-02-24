# 1. 内购配置沙盒测试获取不到数据

```
 func fetchProducts() {
        let productIdentifiers = Set(["com.music.linyu.ancientpoetry.coin700", "com.music.linyu.ancientpoetry.coin800"]) // 替换为你的产品ID
        self.productRequest = SKProductsRequest(productIdentifiers: productIdentifiers)
        self.productRequest?.delegate = self
        self.productRequest?.start()
    }
 
    // 代理回调
 func productsRequest(_ request: SKProductsRequest, didReceive response: SKProductsResponse) {
        print("lt -- products : \(response.products.count)")
        DispatchQueue.main.async {
            self.products = response.products
        }
    }

    func request(_ request: SKRequest, didFailWithError error: Error) {
        print("请求失败: \(error.localizedDescription)")
    }
```

问题： 获取到数据为0个。 即为没有获取到数据



#### 可能1：

productId 没有对应上



#### 可能2：&#x20;

商务没有填写好,

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

如果是这个页面说明没有填写信用卡，、

上面显示“编辑法律实体”,可能就是我们默认的信息出现了问题，点击进去编辑，有红线警告的。比如文本较长。

编辑法律实体正确之后，就会有邀请填写银行卡的内容。&#x20;

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

填写上有关法务的内容。



#### 可能3：点击了 “添加以供审核” —— 要求我们填写的信息以及商品都需要经过审核，所以不要点击。

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>





**参考链接：**

[https://juejin.cn/post/7239962972506996796](https://juejin.cn/post/7239962972506996796)&#x20;

[https://juejin.cn/post/7046969127205863438](https://juejin.cn/post/7046969127205863438)









