# import 导入模块

可以通过 `import` 语句导入其他文件（模块）。以下是一些常见的方法：

1.  **导入整个模块**：

    ```python
    import module_name
    ```
2.  **从模块中导入特定函数或类**：

    ```python
    from module_name import function_name
    ```
3.  **导入模块并重命名**：

    ```python
    import module_name as alias_name
    ```
4.  **导入模块中的所有内容**（不推荐，容易导致命名冲突）：

    ```python
    from module_name import *
    ```
5.  **如果文件在同一目录下**，只需使用文件名（不带 `.py` 后缀）：

    ```python
    import my_file  # 假设 my_file.py 是要导入的文件
    ```
6.  **如果文件在不同目录**，可以通过添加路径或使用包结构来导入。例如，使用相对导入：

    ```python
    from .. import another_module  # 导入上级目录中的模块
    ```

确保被导入的文件（模块）在 Python 的搜索路径中，或者在当前工作目录下。
