# 使用注意事项

### 使用注意事项

1. 忘了在一条调试用的 printf 语句后面跟一个 fflush 调用。
2. 不检查 fopen 函数的返回值。
3. 改变文件的位置将丢弃任何被退回到流的字符。
4. 在使用 fgets 时指定太小的缓冲区。
5. 使用 gets 的输入溢出缓冲区且未被检测到。
6. 使用任何 scanf 系列函数时，格式代码和参数指针类型不匹配。
7. 在任何 scanf 系列函数的每个非数组、非指针参数前忘了加上&符号。
8. 注意在使用 scanf 系列函数转换 double、long double、short 和 long 整型时，在格式代码中加上合适的限定符。
9. sprintf 函数的输出溢出了缓冲区且未检测到。
10. 混淆 printf 和 scanf 格式代码。
11. 使用任何 printf 系列函数时，格式代码和参数类型不匹配。
12. 在有些长整数长于普通整数的机器上打印长整数值时，忘了在格式代码中指定 l 修改符。
13. 使用自动数组作为流的缓冲区时应多加小心。



### 编程提示的总结

1. 在可能出现错误的场合，检查并报告错误。
2. 操纵文本行而无需顾及它们的外部表示形式这个能力有助于提高程序的可移植性。
3. 使用 scanf 限定符提高可移植性。
4. 当你打印长整数时，即使你所使用的机器并不需要，坚持使用 l 修改符可以提高可移植性。


