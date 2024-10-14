# RACSubject



{% hint style="info" %}
重点：

1、继承了RACSignal类， 并且没有重写它的任何方法

2、遵循了[RACSubscriber协议](../../racsubscriber.md)，并且实现了sendNext, sendCompled, sendError 这几个方法,

3、发送消息的时候，遍历subscribers数组，然后一个一个发送出去。
{% endhint %}

####



