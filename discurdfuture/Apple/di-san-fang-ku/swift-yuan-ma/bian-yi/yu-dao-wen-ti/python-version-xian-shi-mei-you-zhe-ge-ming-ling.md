# python --version 显示没有这个命令

因为我们去掉了conda环境，很可能我们以前默认就是使用conda上的python，

这个时候我们要重新链接<mark style="color:red;">**最新的python版本**</mark>

因为没有默认的python命令，将最新的python3版本软链接到python命令中

## 如果在 /usr/local/bin/ &#x20;

ln -s $(which python3) /usr/local/bin/python

<mark style="color:red;">设置在常规的默认的二进制命令目录下</mark>

## 或者在 /opt/homebrew/bin/

ln -s $(which python3)  /opt/homebrew/bin/python

设<mark style="color:orange;">置在python的二进制目录下</mark>



python --version&#x20;

执行这个命令检测python环境是否安装好了。

