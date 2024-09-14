# Python环境的安装

## 1、直接安装

### Mac电脑上

本来就带有



### Windows上

直接下载安装包安装



## 2、通过conda创建独立的项目环境

先装conda，然后通过conda创建对应的python环境可以设置python的版本



常见的是：

```
conda create -n xx【名字】 python=版本号
conda activate xx 激活这个环境
```

在Windows上，通过大概conda的图形界面启动终端。



## 3、安装requirements.txt

### 3.1 通过pip安装

```
pip install -r requirements.txt
```

### 3.2 通过conda安装



但是这里存在一个问题，如果requirements.txt中的包不可用，则会抛出“无包错误”。 使用下面这个命令可以解决这个问题

```
while read requirement; do conda install --yes $requirement; done < requirements.txt
```

或

```
#  Install via `conda` directly.
#  This will fail to install all
#  dependencies. If one fails,
#  all dependencies will fail to install.
conda install --yes --file requirements.txt
```

如果想要在conda命令无效时使用pip命令来代替，那么使用如下命令：

```
while read requirement; do conda install --yes $requirement || pip install $requirement; done < requirements.txt 
```



{% hint style="info" %}
通过conda，我们可以创建不同的python的版本环境来执行不同的项目， —— 推荐
{% endhint %}



