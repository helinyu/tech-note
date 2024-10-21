# RACSubscriber

RACSubscriber 具有协议也有类；&#x20;



### 协议定义了4个方法：

1. `sendNext:` 发送**下一个值**给订阅者。
2. `sendError:` 发送**错误**并终止订阅。
3. `sendCompleted` **完成**订阅并终止。
4. `didSubscribeWithDisposable:` 向订阅者发送表示其订阅之一的可释放对象。任何错误或完成事件必须终止所有订阅。【销毁对象有关】 暂时不管



### 类实现

> 实现协议的4个方法的同时，也提供了一个类方法创建RACSubscriber对象

1. **初始化订阅者**：通过`+subscriberWithNext:error:completed:`方法创建一个订阅者实例，并设置处理`next`、`error`和`completed`事件的回调。【<mark style="color:orange;">拷贝传进来的block到对象的属性中</mark>】
2.

    ```objective-c
    - (void)sendNext:(id)value {
    	@synchronized (self) {
    		void (^nextBlock)(id) = [self.next copy];
    		if (nextBlock == nil) return;

    		nextBlock(value);
    	}
    }
    使用 @synchronized 确保线程安全。
    复制并获取 self.next 闭包。
    判断闭包是否为空，若为空则返回。
    执行闭包并传入参数 value。
    ```

其他的两个方法类似。&#x20;

