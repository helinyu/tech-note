# 环境

## 1、安装



### 方式1：

```
brew install scala
```

### 方式2：

```
brew install coursier && coursier setup 
```

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

这个就是包括了很多的命令行。



## 2、验证

### 1、创建第一个项目

运行命令 `sbt new scala/scala3.g8` 创建 Scala 3 项目，或运行 `sbt new scala/hello-world.g8` 创建 Scala 2 项目。这将从 GitHub 拉取项目模板。

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

运行项目：

```
sbt run 
```

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

到这里，验证了scala的开发环境成功了。



## 3、编辑IDE

常见的IDE：

1、官方有没有提供

2、vscode&#x20;



### 小结：

推荐使用第二种安装工具集



常见步骤：

1、安装开发需要的程序：1》 直接二进制文件 2》工具：brew安装，curl 等工具

2、创建第一个项目，验证安装成功

3、编辑代码工具： 1》官方提供 2》vscode+插件



