# 长度(个数)



在 C 语言中，可以通过以下几种方式确定数组的长度：

**一、使用常量表达式定义数组时已知长度**

```c
int arr[5];
int length = sizeof(arr) / sizeof(arr[0]);
printf("数组长度为：%d\n", length);
```

这里 `sizeof(arr)` 返回整个数组占用的字节数，`sizeof(arr[0])` 返回数组中单个元素占用的字节数，两者相除得到数组的长度。

<mark style="color:orange;">`sizeof`</mark><mark style="color:orange;">主要用于确定类型或变量所占用的字节数</mark>



**二、动态分配的数组（使用 `malloc`、`calloc` 等分配）**

```c
int *dynArr = (int *)malloc(5 * sizeof(int));
int length = 5; // 这里长度是在分配时指定的，也可以用一个变量记录这个长度
printf("动态分配数组长度为：%d\n", length);
free(dynArr);
```

**三、字符串（以 `'\0'` 结尾的字符数组）的长度**

```c
char str[] = "Hello";
int length = 0;
while (str[length]!= '\0') {
    length++;
}
printf("字符串长度为：%d\n", length);
```

需要注意的是，对于函数参数中传递的数组，其会退化为指针，无法直接确定数组的长度，通常需要另外传递数组的长度信息。
