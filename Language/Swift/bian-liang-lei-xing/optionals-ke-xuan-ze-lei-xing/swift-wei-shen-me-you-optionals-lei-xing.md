# swift为什么有optionals类型？

Swift 引入 Optional 类型主要是出于以下几个原因：

1. **安全性**：Swift 是一种类型安全的编程语言，它要求开发者在编译时明确变量的类型。Optional 类型提供了一种方式来处理那些可能不存在或尚未被赋值的值。这有<mark style="color:red;">**助于避免在运行时出现空指针异常**</mark>（null pointer exceptions），这是许多其他编程语言（如 Java、C++ 在使用指针或未初始化的引用时）中常见的错误。
2. **明确性**：通过使用 Optional，开发者可以明确地知道某个值是否可能为 nil。这增加了代码的清晰度和可维护性，因为你可以通过检查 Optional 是否包含值来避免潜在的错误。
3. **简洁性**：Swift 的 Optional 语法相对简洁，使用 `?` 来表示一个值可能是 Optional 的，使用 `!` 来强制解包（但应谨慎使用，因为它可能导致运行时错误）。此外，Swift 提供了丰富的 API 来处理 Optional，如 `if let`、`guard let`、`??` 运算符等，这些工具使得处理 Optional 值既安全又方便。
4. **鼓励更好的编程习惯**：通过强制开发者显式地处理可能为 nil 的情况，<mark style="color:orange;">Optional 鼓励开发者编写更加健壮和可靠的代码</mark>。它促使开发者考虑所有可能的值（包括 nil），并相应地编写代码来处理这些情况。
5. **与 Objective-C 的互操作性**：Swift 设计之初就考虑到了与 Objective-C 的互操作性。由于 Objective-C 广泛使用 nil 来表示缺失的值，Swift 的 Optional 类型提供了一种桥接这两种语言的方式，使得 Swift 代码可以安全地调用 Objective-C 代码，并处理 Objective-C 返回的可能为 nil 的值。

总之，Swift 的 Optional 类型是一种强大的特性，它提高了代码的安全性、明确性和可维护性，同时鼓励开发者编写更加健壮和可靠的代码。



## 小结：

1、有助于判断是否有空指针，所以安全

2、增加了这个内容，并不复杂，在OC里面这个值可能为nil， 而swift中只有加上？才可能是可选类型， 而没有的明确是部位nil的， 所以很明确，没有模棱两可，将是是而非的情况缩小确定。

3、增加了可选类型后，我们还是要判断的，swift提供了if , let, guard let，?? 运算符等可以判断，看是增多，其实并不多，因为在OC中全部都是的时候，都要判断的额，而现在少了，并且提供判断的方法还多。

4、股利更好的编程习惯，也就是我们在编写代码的完整性更好

5、和OC中的nil桥接对应上。
