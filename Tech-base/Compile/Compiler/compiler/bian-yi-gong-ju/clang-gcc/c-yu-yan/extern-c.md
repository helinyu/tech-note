# extern "C"

{% code title="extern "C"宏定义" %}
```
#ifdef __cplusplus
 #define CI_EXTERN_C_BEGIN  extern "C" {
 #define CI_EXTERN_C_END  }
#else
 #define CI_EXTERN_C_BEGIN
 #define CI_EXTERN_C_END

#endif

#ifdef __cplusplus
# define CORE_IMAGE_EXPORT extern "C" __attribute__((visibility("default")))
#else
# define CORE_IMAGE_EXPORT extern __attribute__((visibility("default")))
#endif

#define CORE_IMAGE_CLASS_EXPORT __attribute__((visibility("default")))
```
{% endcode %}

这样CI\_EXTERN\_C\_BEGIN 和 CI\_EXTERN\_C\_END 就可以放在文件的开头和结尾，定义C的内容， 而不用像下面的写法

```
extern "C" {
    #include "some_c_library.h"  // 引入 C 库头文件
}
```



`extern "C"` 是 C++ 中用来支持 C 语言代码和库的关键字。当 C++ 代码中引用了 C 语言代码或 C 语言编写的库时，`extern "C"` 可以告诉编译器该部分代码采用 C 语言的方式进行编译和链接，从而避免 C++ 名称修饰（name mangling）的问题。

#### 为什么需要 `extern "C"`

C++ 编译器在编译时会对函数名称进行修饰（name mangling），将函数名称修改为包含类型信息的复杂名称，以支持函数重载。然而，C 语言不支持函数重载，且不进行名称修饰。这导致直接在 C++ 中调用 C 函数会出现无法找到正确函数的错误。

#### 使用方法

```cpp
// C++代码
extern "C" {
    #include "some_c_library.h"  // 引入 C 库头文件
}

// 或者用于单个函数
extern "C" int c_function(int a);
```

* `extern "C"` 后可以跟花括号 `{}` 包含多行代码。
* 这样编译器会按照 C 语言的方式来处理 `extern "C"` 中的函数或变量定义。

#### 实际应用

在混合 C 和 C++ 编程中，如果我们要用 C++ 调用 C 语言编写的库，比如 POSIX 库或者其他 C 库，`extern "C"` 非常有用。
