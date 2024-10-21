# 编译

看官方提供的文档 [https://github.com/hly-code-source/swift/blob/main/docs/HowToGuides/GettingStarted.md#using-ninja-with-xcode](https://github.com/hly-code-source/swift/blob/main/docs/HowToGuides/GettingStarted.md#using-ninja-with-xcode)



## 构建xcode编译swift源码的过程

### 1、执行构建用于xcode调试的编译命令

{% code title="执行命令" %}
```
utils/build-script --skip-build-benchmarks 
--swift-darwin-supported-archs "$(uname -m)" 
--release-debuginfo --swift-disable-dead-stripping 
--bootstrapping=hosttools 
--sccache 
--xcode --clean
```
{% endcode %}

[命令参数解释](ming-ling-can-shu-jie-shi.md)



