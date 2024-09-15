# del 语句

在 Python 中，`del` 语句用于删除对象。

以下是一些主要的用法：

**一、删除变量**

```python
x = 10
del x
# 这里再访问 x 会引发 NameError，因为 x 已被删除
```

**二、删除列表中的元素**

```python
my_list = [1, 2, 3, 4]
del my_list[1]  # 删除索引为 1 的元素，即 2
print(my_list)  # [1, 3, 4]
```

**三、删除字典中的键值对**

```python
my_dict = {'a': 1, 'b': 2, 'c': 3}
del my_dict['b']
print(my_dict)  # {'a': 1, 'c': 3}
```

**四、删除切片**

对于列表、元组等序列类型，可以使用 `del` 语句删除一个切片：

```python
my_list = [1, 2, 3, 4, 5]
del my_list[1:3]
print(my_list)  # [1, 4, 5]
```

需要注意的是，`del` 只是删除了对对象的引用，当一个对象不再被任何引用指向时，Python 的垃圾回收机制会在适当的时候回收该对象所占用的内存空间。
