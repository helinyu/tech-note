# 结构体

在 C 语言中，结构体（struct）是一种用户自定义的数据类型，它可以将不同类型的数据组合在一起，形成一个新的复合数据类型。

**一、结构体的定义**

结构体的定义形式如下：

```c
struct 结构体名 {
    成员类型1 成员名1;
    成员类型2 成员名2;
   ...
    成员类型n 成员名n;
};
```

例如：

```c
struct Person {
    char name[50];
    int age;
    float height;
};
```

这里定义了一个名为`Person`的结构体，它包含三个成员：一个字符数组`name`用来存储人的名字，一个整数`age`表示年龄，一个浮点数`height`表示身高。

**二、结构体变量的声明和初始化**

1.  声明结构体变量：

    * 可以在定义结构体后声明结构体变量，例如：

    ```c
    struct Person p1;
    ```

    * 也可以在定义结构体的同时声明变量，例如：

    ```c
    struct Person {
        char name[50];
        int age;
        float height;
    } p2;
    ```
2.  初始化结构体变量：

    * 可以在声明变量时进行初始化，例如：

    ```c
    struct Person p3 = {"John", 30, 1.75};
    ```

    * 也可以使用指定初始化器进行初始化，这种方式更加灵活，可以不按照结构体成员的定义顺序进行初始化，例如：

    ```c
    struct Person p4 = {.age = 25,.height = 1.80,.name = "Alice"};
    ```

**三、结构体成员的访问**

可以使用点运算符（`.`）来访问结构体变量的成员，例如：

```c
struct Person p = {"Bob", 28, 1.78};
printf("Name: %s\n", p.name);
printf("Age: %d\n", p.age);
printf("Height: %.2f\n", p.height);
```

也可以使用指针和箭头运算符（`->`）来访问结构体变量的成员，例如：

```c
struct Person *ptr = &p;
printf("Name: %s\n", ptr->name);
printf("Age: %d\n", ptr->age);
printf("Height: %.2f\n", ptr->height);
```

**四、结构体的嵌套**

结构体可以嵌套其他结构体，例如：

```c
struct Address {
    char city[50];
    char state[50];
};

struct Person {
    char name[50];
    int age;
    float height;
    struct Address addr;
};
```

在这个例子中，`Person`结构体中嵌套了一个`Address`结构体，表示一个人的地址信息。

**五、结构体的作用**

1. 数据封装：结构体可以将相关的数据组合在一起，提高代码的可读性和可维护性。
2. 数据传递：结构体可以作为函数的参数或返回值，方便地传递一组相关的数据。
3. 模拟面向对象编程：虽然 C 语言不是面向对象编程语言，但可以使用结构体和函数指针来模拟一些面向对象编程的特性，如封装、继承和多态。

总之，结构体是 C 语言中非常有用的一种数据类型，可以帮助程序员更好地组织和管理数据。
