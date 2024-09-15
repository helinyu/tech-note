# 作为参数传递



**一、传递数组名（实际上传递的是指向数组首元素的指针）「同C一样」**

```cpp
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    printArray(arr, size);
    return 0;
}
```

**二、使用指针参数传递数组 「同C一样」**

与传递数组名类似，效果是一样的。

```cpp
void printArray(int* arr, int size) {
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    printArray(arr, size);
    return 0;
}
```

**三、传递数组的引用**

这种方式可以明确地知道传递的是一个数组，并且避<mark style="color:red;">**免了数组退化为指针的情况**</mark>。

相当于写死了长度，这样是很不好的，要想传递长度，还是得使用模板参数传递。

<pre class="language-cpp"><code class="lang-cpp"><strong>void printArray(int(&#x26;arr)[5]) {
</strong>    for (int i = 0; i &#x3C; 5; i++) {
        std::cout &#x3C;&#x3C; arr[i] &#x3C;&#x3C; " ";
    }
    std::cout &#x3C;&#x3C; std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    printArray(arr);
    return 0;
}
</code></pre>

注意，在这种方式中，必须明确指定数组的大小，否则会导致编译错误。

**四、使用模板参数推导传递数组 【推荐】**

#### 1、可以使用模板函数来自动推导数组的大小。

```cpp
template <typename T, size_t N>
void printArray(T(&arr)[N]) {
    for (size_t i = 0; i < N; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    printArray(arr);
    return 0;
}
```



#### **2、使用模板函数和迭代器**

```cpp
#include <iostream>
#include <iterator>

template<typename T>
void processArray(T arr[]) {
    int length = std::distance(std::begin(arr), std::end(arr));
    std::cout << "Length of array: " << length << std::endl;
    for (int i = 0; i < length; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    processArray(arr);
    return 0;
}
```

这种方式利用了迭代器来计算数组的长度。但需要注意的是，这里的实现假设传入的数组有明确的结束位置，不能是未初始化或不完整的数组。



五、**传递数组的引用，并在调用函数中计算长度**

**也就相当于传递了结束符，也相当于传递了多一个参数。**

```cpp
#include <iostream>

void processArray(int(&arr)[], int* endPtr) {
    int length = endPtr - arr;
    std::cout << "Length of array: " << length << std::endl;
    for (int i = 0; i < length; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    processArray(arr, std::end(arr));
    return 0;
}
```

这里使用了`std::end(arr)`来获取数组末尾的指针，通过计算与数组首地址的差值得到长度。

## 小结：

C++要想和其他现代语言一样，通过传递数组的名字，就能够传递过去数组(包括长度)， 就要使用模板参数。



<mark style="color:red;">**综上： 还是传模板比较好。**</mark>
