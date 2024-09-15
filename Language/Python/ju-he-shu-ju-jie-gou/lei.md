# 类

在 Python 中，类（Class）是一种用于创建对象的模板或蓝图。它定义了对象的属性（数据）和方法（行为）。

以下是一个关于 Python 类的详细介绍：

**一、定义类**

```python
class Dog:
    # 类属性
    species = "Canis lupus familiaris"

    # 构造方法
    def __init__(self, name, age):
        # 实例属性
        self.name = name
        self.age = age

    # 实例方法
    def bark(self):
        print(f"{self.name} says woof!")

    # 另一个实例方法
    def describe(self):
        print(f"{self.name} is {self.age} years old.")
```

在上面的例子中，我们定义了一个名为 `Dog` 的类。它有一个类属性 `species`，表示狗的物种。构造方法 `__init__` 在创建对象时被自动调用，用于初始化实例属性 `name` 和 `age`。`bark` 和 `describe` 是实例方法，用于定义狗的行为。

**二、创建对象（实例化）**

```python
my_dog = Dog("Fido", 3)
your_dog = Dog("Buddy", 5)
```

这里我们创建了两个 `Dog` 类的对象 `my_dog` 和 `your_dog`。

**三、访问属性和方法**

1. 访问属性：

```python
print(my_dog.name)  # Fido
print(your_dog.age)  # 5
print(my_dog.species)  # Canis lupus familiaris
print(your_dog.species)  # Canis lupus familiaris
```

2. 调用方法：

```python
my_dog.bark()  # Fido says woof!
your_dog.describe()  # Buddy is 5 years old.
```

**四、类的继承**

Python 支持类的继承，允许创建一个新类从现有的类继承属性和方法。

```python
class GoldenRetriever(Dog):
    def fetch(self):
        print(f"{self.name} is fetching.")
```

在这个例子中，`GoldenRetriever` 类继承自 `Dog` 类。它继承了 `Dog` 类的所有属性和方法，并添加了一个新方法 `fetch`。

```python
my_golden = GoldenRetriever("Max", 2)
print(my_golden.species)  # Canis lupus familiaris
my_golden.bark()  # Max says woof!
my_golden.fetch()  # Max is fetching.
```

**五、特殊方法（魔法方法）**

Python 中的类可以定义特殊方法，这些方法以双下划线开头和结尾。例如，`__str__` 方法可以定义对象的字符串表示形式。

```python
class Dog:
    #...

    def __str__(self):
        return f"{self.name}, {self.age} years old"
```

```python
my_dog = Dog("Fido", 3)
print(my_dog)  # Fido, 3 years old
```

类在 Python 中是面向对象编程的基础，它允许你组织代码、提高代码的可维护性和可扩展性。

