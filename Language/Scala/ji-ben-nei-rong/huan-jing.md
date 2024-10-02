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

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

这个就是包括了很多的命令行。



## 2、验证

### 1、创建第一个项目

运行命令 `sbt new scala/scala3.g8` 创建 Scala 3 项目，或运行 `sbt new scala/hello-world.g8` 创建 Scala 2 项目。这将从 GitHub 拉取项目模板。

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

运行项目：

```
sbt run 
```

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

到这里，验证了scala的开发环境成功了。

### 小结：

推荐使用第二种安装工具集



