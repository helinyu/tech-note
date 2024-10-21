# 一个NSObject对象占用多少内存？

系统分配了16个字节给NSObject对象（通过malloc\_size函数获得）&#x20;

但NSObject对象内部只使用了8个字节的空间（64bit环境下，可以通过class\_getInstanceSize函数获得）

