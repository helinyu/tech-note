# 字符串

在 Python 中，字符串（`str`）是一种非常重要的内置数据类型，主要用于处理文本。Python 没有单独的字符类型，字符在 Python 中实际上就是长度为 1 的字符串。

#### 1. **字符串的定义**

在 Python 中，字符串可以使用**单引号** (`'`) 或 **双引号** (`"`) 来定义。例如：

```python
s1 = 'Hello'
s2 = "World"
```

两者没有区别，可以根据需要选择合适的引号。

#### 2. **多行字符串**

如果需要定义多行字符串，可以使用**三引号** (`'''` 或 `"""`)：

```python
s = '''This is
a multi-line
string.'''
```

或者：

```python
s = """This is
a multi-line
string."""
```

#### 3. **转义字符**

在字符串中，可以使用反斜杠 (`\`) 来引入转义字符。例如：

* ：换行
* ：制表符
* `\\`：反斜杠本身
* `\'` 或 `\"`：单引号或双引号

示例：

```python
s = "Hello\nWorld"  # 换行
print(s)
# 输出：
# Hello
# World
```

#### 4. **原始字符串**

在处理正则表达式或路径时，常常需要避免转义字符的干扰。这时可以使用原始字符串（以 `r` 或 `R` 开头），这样反斜杠将不再具有特殊意义：

```python
s = r'C:\Users\name'  # 原始字符串
print(s)
# 输出：C:\Users\name
```

#### 5. **字符串的基本操作**

**(1) 拼接**

使用 `+` 进行字符串拼接：

```python
s = 'Hello' + ' ' + 'World'
print(s)  # 输出：Hello World
```

**(2) 重复**

使用 `*` 将字符串重复多次：

```python
s = 'Hello' * 3
print(s)  # 输出：HelloHelloHello
```

**(3) 索引和切片**

字符串可以像列表一样进行索引和切片，索引从 0 开始：

```python
s = 'Python'
print(s[0])   # 输出：P
print(s[-1])  # 输出：n，负数索引从右边开始

# 切片
print(s[1:4]) # 输出：yth，从索引1到索引4（不包括4）
print(s[:3])  # 输出：Pyt，从开始到索引3（不包括3）
print(s[3:])  # 输出：hon，从索引3到末尾
```

**(4) 长度**

使用 `len()` 函数可以获取字符串的长度：

```python
s = 'Hello'
print(len(s))  # 输出：5
```

#### 6. **字符串常用方法**

Python 提供了很多字符串处理的方法，常见的方法有：

**(1) `lower()` 和 `upper()`**

将字符串转换为小写或大写：

```python
s = 'Hello'
print(s.lower())  # 输出：hello
print(s.upper())  # 输出：HELLO
```

**(2) `strip()`**

移除字符串两端的空白字符（或指定字符）：

```python
s = '  Hello  '
print(s.strip())  # 输出：Hello
```

**(3) `split()`**

将字符串按指定的分隔符拆分成列表：

```python
s = 'a,b,c'
print(s.split(','))  # 输出：['a', 'b', 'c']
```

**(4) `join()`**

用指定的字符串将列表中的元素连接起来：

```python
lst = ['a', 'b', 'c']
print(','.join(lst))  # 输出：a,b,c
```

**(5) `replace()`**

替换字符串中的某些子字符串：

```python
s = 'Hello, World'
print(s.replace('World', 'Python'))  # 输出：Hello, Python
```

**(6) `find()` 和 `index()`**

用于查找子字符串的位置：

* `find()`：返回子字符串的第一个位置，如果没有找到则返回 `-1`。
* `index()`：返回子字符串的第一个位置，如果没有找到则抛出异常。

```python
s = 'Hello, World'
print(s.find('World'))  # 输出：7
print(s.find('Python'))  # 输出：-1
```

**(7) `startswith()` 和 `endswith()`**

检查字符串是否以指定的前缀或后缀开始/结束：

```python
s = 'Hello, World'
print(s.startswith('Hello'))  # 输出：True
print(s.endswith('World'))    # 输出：True
```

#### 7. **字符串的不可变性**

Python 中的字符串是**不可变**的。这意味着一旦创建，字符串的内容就不能被修改。如果对字符串进行操作，结果会生成一个新的字符串，而不是对原字符串进行修改。

```python
s = 'Hello'
s[0] = 'h'  # 会抛出错误，因为字符串不可变
```

#### 8. **格式化字符串**

Python 支持多种方式对字符串进行格式化：

**(1) 使用 `%` 格式符：**

```python
name = 'Alice'
age = 25
print('My name is %s and I am %d years old' % (name, age))
# 输出：My name is Alice and I am 25 years old
```

**(2) 使用 `str.format()`：**

```python
name = 'Alice'
age = 25
print('My name is {} and I am {} years old'.format(name, age))
# 输出：My name is Alice and I am 25 years old
```

**(3) 使用 f-strings (Python 3.6+)：**

```python
name = 'Alice'
age = 25
print(f'My name is {name} and I am {age} years old')
# 输出：My name is Alice and I am 25 years old
```

#### 9. **字符**

Python 中没有单独的字符类型，字符被认为是长度为1的字符串。你可以通过索引获取字符串中的某个字符：

```python
s = 'Hello'
char = s[0]  # 'H'，这是一个长度为1的字符串
```

#### 总结：

* **字符串**是 Python 中的不可变数据类型，可以通过单引号、双引号或三引号定义。
* **字符**在 Python 中是长度为1的字符串，没有独立的字符类型。
* Python 提供了丰富的字符串处理方法，如拼接、切片、大小写转换、查找、替换等，适用于各种文本处理场景。









## 小结：

1、现在都没有字符的概念了，只有单个字符的字符串了

2、引号上的使用 单引号、栓引号、三引号

3、字符串都是不可变的了，改变就会生成一个新的对象返回。

4、转义符应该都是没有变化的

