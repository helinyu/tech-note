# 常见文件格数数据处理

在 Python 中，可以使用多种方式来存储文件，不同的文件格式有不同的存储和读取方法。以下是一些常见的文件格式及其存储方式：

**一、文本文件（.txt）**

1.  写入文本文件：

    使用 `open()` 函数以写入模式（`'w'`）打开文件，然后使用 `write()` 方法写入内容。

    ```python
    with open('example.txt', 'w') as file:
        file.write('Hello, world!')
    ```
2.  读取文本文件：

    使用 `open()` 函数以读取模式（`'r'`）打开文件，然后使用 `read()`、`readline()` 或 `readlines()` 方法读取内容。

    ```python
    with open('example.txt', 'r') as file:
        content = file.read()
        print(content)
    ```

**二、CSV 文件（.csv）**

Python 中有内置的 `csv` 模块来处理 CSV 文件。

1.  写入 CSV 文件：

    ```python
    import csv

    data = [['Name', 'Age'], ['Alice', '25'], ['Bob', '30']]

    with open('example.csv', 'w', newline='') as file:
        writer = csv.writer(file)
        writer.writerows(data)
    ```
2.  读取 CSV 文件：

    ```python
    import csv

    with open('example.csv', 'r') as file:
        reader = csv.reader(file)
        for row in reader:
            print(row)
    ```

**三、JSON 文件（.json）**

Python 中的 `json` 模块用于处理 JSON 格式的数据。

1.  写入 JSON 文件：

    ```python
    import json

    data = {'name': 'Alice', 'age': 25}

    with open('example.json', 'w') as file:
        json.dump(data, file)
    ```
2.  读取 JSON 文件：

    ```python
    import json

    with open('example.json', 'r') as file:
        data = json.load(file)
        print(data)
    ```

**四、Pickle 文件（.pkl）**

`pickle` 模块可以用来序列化和反序列化 Python 对象。

1.  写入 Pickle 文件：

    ```python
    import pickle

    data = [1, 2, 3, 4, 5]

    with open('example.pkl', 'wb') as file:
        pickle.dump(data, file)
    ```
2.  读取 Pickle 文件：

    ```python
    import pickle

    with open('example.pkl', 'rb') as file:
        data = pickle.load(file)
        print(data)
    ```

每种文件格式都有其特定的用途和优势，选择合适的文件格式取决于你的具体需求。
