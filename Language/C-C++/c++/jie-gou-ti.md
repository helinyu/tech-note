# 结构体

C++中也有结构体（struct）。C++中的结构体与C语言中的结构体有一些区别：

**一、默认访问权限**

* C 语言结构体：成员的默认访问权限是公有（public）的。
* C++结构体：成员的默认访问权限也是公有，但 C++中的结构体可以像类一样定义成员函数，并且可以设置成员的访问权限为私有（private）、保护（protected）等。

例如：

```cpp
// C++
struct MyStruct {
private:
    int privateMember;
public:
    void setPrivateMember(int value) {
        privateMember = value;
    }
    int getPrivateMember() const {
        return privateMember;
    }
};
```

**二、与类的关系**

在 C++中，结构体和类（class）非常相似，唯一的区别是默认的访问权限不同。类的默认成员访问权限是私有，而结构体是公有。

```cpp
class MyClass {
    // 默认私有成员
public:
    void someFunction();
};

struct MyStruct {
    // 默认公有成员
    void someFunction();
};
```

**三、模板支持**

C++中的结构体可以作为模板参数，就像类一样。

```cpp
template <typename T>
struct MyTemplateStruct {
    T data;
};
```

**四、继承和多态**

C++中的结构体可以参与继承和多态，与类的使用方式类似。

```cpp
struct BaseStruct {
    virtual void print() const {
        std::cout << "BaseStruct\n";
    }
};

struct DerivedStruct : BaseStruct {
    void print() const override {
        std::cout << "DerivedStruct\n";
    }
};
```

总的来说，C++中的结构体在功能上比 C 语言中的结构体更强大，可以像类一样使用，具有更多的特性和灵活性。
