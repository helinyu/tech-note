# 环境

## 1、[MacOS上的安装](https://www.rust-lang.org/zh-CN/learn/get-started)

#### 安装命令：

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

安装完成显示：

```
Rust is installed now. Great!
```

#### 查看版本(不同的额工具)

{% code overflow="wrap" lineNumbers="true" %}
```
rustup --version 
rustc -V
cargo -V
```
{% endcode %}

#### 更新

```
rustup update
```

#### 卸载

```
rustup self uninstall
```

***

在Visual code中安装rust环境，直接在插件里面搜索rust；

选择社区驱动的rust-analyzer插件安装即可



cargo工具的命令行：

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

***

## 2、创建第一个rust项目并且运行，测试基本环境的成功

```
cargo new hello-rust // 创建rust的基本项目成功
cargo run // 运行这个项目
xx 都是cargo命令： 无非就 测试、构建、发布 等等 运行打包的命令
```



## 安装可能遇到的问题

[问题1](https://github.com/rust-lang/rustup/issues/953)
