# 访问元素

1. 使用下标：
   * 数组下标从 0 开始。例如，对于数组`int arr[5]`，可以使用`arr[0]`访问第一个元素，`arr[1]`访问第二个元素，以此类推。
   *   可以通过循环遍历数组并使用下标来访问每个元素。例如：

       ```c
       int arr[5] = {1, 2, 3, 4, 5};
       for (int i = 0; i < 5; i++) {
           printf("%d ", arr[i]);
       }
       ```
2. 使用指针：
   * 数组名本身就是一个指向数组第一个元素的指针。可以使用指针算术来访问数组元素。
   *   例如：

       ```c
       int arr[5] = {1, 2, 3, 4, 5};
       int *ptr = arr;
       printf("%d ", *(ptr + 0)); // 相当于 arr[0]
       printf("%d ", *(ptr + 1)); // 相当于 arr[1]
       ```
   *   也可以使用指针遍历数组：

       ```c
       int arr[5] = {1, 2, 3, 4, 5};
       int *ptr = arr;
       for (int i = 0; i < 5; i++) {
           printf("%d ", *(ptr + i));
       }
       ```