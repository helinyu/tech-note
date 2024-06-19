# rust 安装环境以及验证

### MacOS上的安装

```
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
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
