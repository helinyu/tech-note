# 迭代器(Iterator)



> 这个需要和while结合一起使用

```
let array = ["A", "B", "C", "D", "E"]
var arrInterator = array.makeIterator()
while let ele = arrInterator.next() {
    print(ele)
}
```

这个就是通过while来不断获取next的元素来判断使用。
