# 1、环境搭建以及开启第一个项目测试

### 方式一

1、通过flutter的源码 下载安装

```
// mac安装flutter
git clone git@github.com:flutter/flutter.git
cd flutter/bin
./dart --version // 这个会安装dart语言的环境
./flutter --version  // 这个会安装flutter的环境
配置命令行为电脑全局可以访问：
pwd // 查看当前bin命令工具的路径
vi ~/.zshrc
将上面的bin路径添加到path中
source ~/.zshrc // 这样配置更新，就可以在其他地方使用命令了
```

2、创建第一个项目验证环境的安装

```
flutter create xx(项目名称)
cd xx && flutter run  // 运行第一个项目
```

3、终端显示你要运行的平台

***

### 方式二、

1、如果要在vs code中安装环境，

在插件里面搜索：flutter 然后安装就可以了，它同时也会安装dart的环境

2、cmd+shift+p ,输入flutter 会出现对应的命令，选择new project ，就会创建一个项目

弹出选项，选择application， 弹出选择工程路径，选择就好了。同样创建了一个项目

3、运行项目，cmd+shift+p ，选择flutter:select device ，选择运行的目标设备然后运行。 然后弹出要选择运行的设备，选择就好了。

4、创建的项目目录结构概览：

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

***

选择了macOS的应用，显示错误为：

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

```
xcrun: error: unable to find utility "xcodebuild", not a developer
tool or in PATH
  Command: xcrun xcodebuild -list -project Runner.xcodeproj
```

让当前的电脑确认接受这个协议：

<pre><code>xcode-select --install // 这个可以不管
sudo xcode-select --reset
<strong>sudo xcodebuild -license accept // 主要这个命令
</strong></code></pre>

***

```
flutter doctor  // 查看flutter运行的环境
```
