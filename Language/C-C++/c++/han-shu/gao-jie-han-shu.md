# 高阶函数

在 C++中，高阶函数是指可以接受函数作为参数或者返回函数的函数。

### **一、使用函数指针实现高阶函数**

1. 接受函数指针作为参数：

以下是一个使用函数指针作为参数的高阶函数示例，用于对一个整数数组进行操作：

```cpp
#include <iostream>

void processArray(int arr[], int size, void (*func)(int)) {
    for (int i = 0; i < size; i++) {
        func(arr[i]);
    }
}

void printValue(int value) {
    std::cout << value << " ";
}

void doubleValue(int value) {
    std::cout << value * 2 << " ";
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Original array: ";
    processArray(arr, size, printValue);
    std::cout << std::endl;

    std::cout << "Doubled array: ";
    processArray(arr, size, doubleValue);
    std::cout << std::endl;

    return 0;
}
```

在这个例子中，`processArray`函数是一个高阶函数，它接受一个整数数组、数组大小和一个函数指针作为参数。这个函数指针指向一个接受一个整数参数并返回 void 的函数。在`main`函数中，分别传入`printValue`和`doubleValue`函数作为参数，对数组进行不同的操作。

2. 返回函数指针：

以下是一个返回函数指针的高阶函数示例：

```cpp
#include <iostream>

int (*selectOperation(char op))(int, int) {
    if (op == '+') {
        return [](int a, int b) { return a + b; };
    } else if (op == '-') {
        return [](int a, int b) { return a - b; };
    } else {
        return nullptr;
    }
}

int main() {
    int (*addFunc)(int, int) = selectOperation('+');
    int (*subFunc)(int, int) = selectOperation('-');

    std::cout << "Addition: " << addFunc(5, 3) << std::endl;
    std::cout << "Subtraction: " << subFunc(5, 3) << std::endl;

    return 0;
}
```

在这个例子中，`selectOperation`函数是一个高阶函数，它根据传入的操作符返回一个指向相应函数的函数指针。这个函数指针指向一个接受两个整数参数并返回一个整数的函数。

### **二、使用函数对象（仿函数）实现高阶函数**

1. 接受函数对象作为参数：

以下是一个使用函数对象作为参数的高阶函数示例：

```cpp
#include <iostream>
#include <algorithm>

class MultiplyBy {
public:
    MultiplyBy(int factor) : factor(factor) {}
    int operator()(int value) const {
        return value * factor;
    }
private:
    int factor;
};

void processArray(int arr[], int size, MultiplyBy multiplyBy) {
    std::transform(arr, arr + size, arr, multiplyBy);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    MultiplyBy multiplyBy3(3);
    processArray(arr, size, multiplyBy3);

    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

在这个例子中，`processArray`函数接受一个整数数组、数组大小和一个函数对象作为参数。函数对象`MultiplyBy`实现了一个可调用的运算符`operator()`，用于对整数进行乘法操作。

2. 返回函数对象：

以下是一个返回函数对象的高阶函数示例：

```cpp
#include <iostream>
#include <functional>

std::function<int(int)> createAdder(int valueToAdd) {
    return [valueToAdd](int value) {
        return value + valueToAdd;
    };
}

int main() {
    std::function<int(int)> add5 = createAdder(5);
    std::function<int(int)> add10 = createAdder(10);

    std::cout << "Add 5 to 3: " << add5(3) << std::endl;
    std::cout << "Add 10 to 7: " << add10(7) << std::endl;

    return 0;
}
```

在这个例子中，`createAdder`函数是一个高阶函数，它接受一个整数作为参数，并返回一个`std::function`对象，这个对象表示一个接受一个整数参数并返回一个整数的函数。返回的函数对象将传入的参数与固定的值相加。

### **三、使用 lambda 表达式实现高阶函数**

1. 接受 lambda 表达式作为参数：

以下是一个使用 lambda 表达式作为参数的高阶函数示例：

```cpp
#include <iostream>
#include <algorithm>

void processArray(int arr[], int size, const std::function<int(int)>& func) {
    std::transform(arr, arr + size, arr, func);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    processArray(arr, size, [](int value) { return value * 2; });

    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

在这个例子中，`processArray`函数接受一个整数数组、数组大小和一个`std::function`对象作为参数。这个`std::function`对象可以接受一个整数参数并返回一个整数，可以用 lambda 表达式来初始化。

2. 返回 lambda 表达式：

以下是一个返回 lambda 表达式的高阶函数示例：

```cpp
#include <iostream>
#include <functional>

std::function<int(int)> createOperation(char op) {
    if (op == '+') {
        return [](int value) { return value + 5; };
    } else if (op == '-') {
        return [](int value) { return value - 3; };
    } else {
        return [](int value) { return value; };
    }
}

int main() {
    std::function<int(int)> addFunc = createOperation('+');
    std::function<int(int)> subFunc = createOperation('-');

    std::cout << "Add 5 to 3: " << addFunc(3) << std::endl;
    std::cout << "Subtract 3 from 7: " << subFunc(7) << std::endl;

    return 0;
}
```

在这个例子中，`createOperation`函数是一个高阶函数，它根据传入的操作符返回一个 lambda 表达式，这个 lambda 表达式接受一个整数参数并返回一个整数。

高阶函数在 C++中可以提高代码的灵活性和可重用性，使代码更加简洁和易于维护。通过使用函数指针、函数对象或 lambda 表达式，可以实现不同类型的高阶函数，满足各种编程需求。

