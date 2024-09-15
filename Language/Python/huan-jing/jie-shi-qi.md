# 解释器



## &#x20;1、可以在shell中运行python程序，使用解释器



1、 解释器的操作方式类似 Unix Shell：用与 tty 设备关联的标准输入调用时，可以交互式地读取和执行命令；以文件名参数，或标准输入文件调用时，则读取并执行文件中的 _脚本_。

\


2、`python -c command [arg] ...`，这将执行 _command_ 中的语句，相当于 shell 的 [`-c`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-c) 选项。 由于 Python 语句经常包含空格或其他会被 shell 特殊对待的字符，通常建议用引号将整个 _command_ 括起来。



3、Python 模块也可以当作脚本使用。输入：`python -m module [arg] ...`，会执行 _module_ 的源文件，这跟在命令行把路径写全了一样。

\
4、 在交互模式下运行脚本文件，只要在脚本名称参数前，加上选项 [`-i`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-i) 就可以了。



### 1、传入参数

解释器读取命令行参数，把脚本名与其他参数转化为字符串列表存到 `sys` 模块的 `argv` 变量里。执行 `import sys`，可以导入这个模块，并访问该列表。\
该列表最少有一个元素；未给定输入参数时，`sys.argv[0]` 是空字符串。

给定脚本名是 `'-'` （标准输入）时，`sys.argv[0]` 是 `'-'`。

使用 [`-c`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-c) _command_ 时，`sys.argv[0]` 是 `'-c'`。

如果使用选项 [`-m`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-m) _module_，`sys.argv[0]` 就是包含目录的模块全名。

解释器不处理 [`-c`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-c) _command_ 或 [`-m`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-m) _module_ 之后的选项，而是直接留在 `sys.argv` 中由命令或模块来处理。

这个其实就是常见的脚本语言的特性\


### 2、交互模式

就是常见的repl的交互式环境 ，&#x20;

其实这个就是一个数字计算器， 可以用来计算使用等等都可以的。



### 3、字符编码

Python 源码文件的编码是 UTF-8

可以用于字符串字面值、变量、函数名及注释 —— 尽管标准库只用常规的 ASCII 字符作为变量名或函数名，可移植代码都应遵守此约定。



#### 3.1 如果不使用默认编码，

则要声明文件的编码，文件的 _第一_ 行要写成特殊注释。句法如下：

```
# -*- coding: encoding -*-
```

其中，_encoding_ 可以是 Python 支持的任意一种 [`codecs`](https://docs.python.org/zh-cn/3/library/codecs.html#module-codecs)。

比如，声明使用 Windows-1252 编码，源码文件要写成：

```
# -*- coding: cp1252 -*-
```



#### _3.2 第一行_ 的规则也有一种例外情况，

源码以 [UNIX "shebang" 行](https://docs.python.org/zh-cn/3/tutorial/appendix.html#tut-scripts) 开头。此时，编码声明要写在文件的第二行。例如：

```
#!/usr/bin/env python3
# -*- coding: cp1252 -*-
```

\


