# 作为参数传递

**数组作为函数参数**\


1. 传递方式：
   * 当数组作为函数参数传递时，实际上传递的是数组的首地址，也就是一个指向数组第一个元素的指针。
   * 例如：`void func(int arr[], int size)`，这里的`arr`实际上是一个指针。
2. 确定数组大小：
   * 由于只传递了地址，函数无法直接知道数组的大小，通常需要另外一个参数来指定数组的大小，或者使用特殊的结束标记（对于字符数组可以使用`'\0'`作为结束标记）。