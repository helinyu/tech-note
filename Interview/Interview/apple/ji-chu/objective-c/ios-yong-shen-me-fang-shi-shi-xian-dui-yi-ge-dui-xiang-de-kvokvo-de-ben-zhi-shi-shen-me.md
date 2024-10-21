# iOS用什么方式实现对一个对象的KVO？(KVO的本质是什么？)

利用RuntimeAPI动态生成一个子类，并且让instance对象的isa指向这个全新的子类&#x20;

当修改instance对象的属性时，会调用Foundation的\_NSSetXXXValueAndNotify函数&#x20;

willChangeValueForKey:&#x20;

父类原来的setter

didChangeValueForKey:&#x20;

内部会触发监听器（Oberser）的监听方法( observeValueForKeyPath:ofObject:change:context:）
