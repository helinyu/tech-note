# Category的使用场合是什么？

**Category的实现原理**&#x20;

Category编译之后的底层结构是struct category\_t，里面存储着分类的对象方法、类方法、属性、协议信息&#x20;

在程序运行的时候，runtime会将Category的数据，合并到类信息中（类对象、元类对象中）



### Category和Class Extension的区别是什么？

Class Extension在编译的时候，它的数据就已经包含在类信息中&#x20;

Category是在运行时，才会将数据合并到类信息中



### Category能否添加成员变量？如果可以，如何给Category添加成员变量？

不能直接给Category添加成员变量，但是可以间接实现Category有成员变量的效果

