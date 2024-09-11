# 1、Rust 安装环境以及验证

### MacOS上的安装



#### 安装命令：

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

&#x20;安装完成显示：&#x20;

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

&#x20;选择社区驱动的rust-analyzer插件安装即可

***

## 安装可能遇到的问题

[问题1](https://github.com/rust-lang/rustup/issues/953)



