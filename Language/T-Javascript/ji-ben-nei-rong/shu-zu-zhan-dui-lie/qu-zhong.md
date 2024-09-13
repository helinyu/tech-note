# 去重

* 可以使用 **`Set`** 去重

```js
js复制代码let arr = [1, 2, 2, 3, 4, 4];
let uniqueArr = Array.from(new Set(arr)); // [1, 2, 3, 4]
```
