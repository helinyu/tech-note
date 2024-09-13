# 对象内容遍历方式

## &#x20;遍历对象的键、值和键值对

对于对象的遍历，除了 `for...in`，还可以使用 `Object.keys()`、`Object.values()` 和 `Object.entries()` 来遍历键、值和键值对。

**示例：**

```javascript
let obj = { name: "Alice", age: 25, job: "developer" };

console.log("Keys:");
Object.keys(obj).forEach(key => console.log(key)); // 输出: name, age, job

console.log("Values:");
Object.values(obj).forEach(value => console.log(value)); // 输出: Alice, 25, developer

console.log("Entries (key-value pairs):");
Object.entries(obj).forEach(([key, value]) => console.log(`${key}: ${value}`));
// 输出:
// name: Alice
// age: 25
// job: developer
```
