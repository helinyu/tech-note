# Endpoint

<figure><img src="../../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **A**：开始转换`Endpoint`为`URLRequest`。
* **B**：根据任务类型进行不同的处理。
* **C**：对于简单的任务类型，直接返回请求。
* **D**：对于`requestData`任务，设置请求体并返回请求。
* **E**：对于`requestJSONEncodable`任务，编码JSON并返回请求。
* **F**：对于`requestCustomJSONEncodable`任务，使用自定义编码器编码JSON并返回请求。
* **G**：对于`requestParameters`任务，编码参数并返回请求。
* **H**：对于`uploadCompositeMultipart`和`uploadCompositeMultipartFormData`任务，编码URL参数并返回请求。
* **I**：对于`downloadParameters`任务，编码下载参数并返回请求。
* **J**：对于`requestCompositeData`任务，设置请求体并编码URL参数返回请求。
* **K**：检查`bodyEncoding`是否为`URLEncoding.httpBody`。
* **L**：编码body参数并返回请求。
* **M**：抛出错误。

