# Trampoline

在编程中，`Trampoline` 是一种用于延迟计算或避免递归溢出的方法。通过 `Trampoline`，递归函数的调用会被转换成一系列的循环调用，从而避免堆栈溢出问题。它也常用于实现惰性计算（lazy evaluation），将嵌套的函数调用展平为迭代调用。
