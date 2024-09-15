# 创建静态数组

1. 定义数组：
   * `数据类型 数组名[数组大小];`
   * 例如：`int arr[5];`定义了一个名为`arr`的整型数组，可以存储 5 个整数。
2. 初始化数组：
   * 可以在定义数组时进行初始化。
   * 例如：`int arr[5] = {1, 2, 3, 4, 5};`。
   * 如果只初始化部分元素，未初始化的元素会被自动初始化为 0（对于数值类型）或空字符（对于字符类型）。例如：`int arr[5] = {1, 2};`，则`arr`中的元素为`1, 2, 0, 0, 0`。