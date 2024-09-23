# 源码编译



[sqlite源码地址](https://github.com/sqlite/sqlite)

```
apt install gcc make tcl-dev  ;#  Make sure you have all the necessary build tools
tar xzf sqlite.tar.gz         ;#  Unpack the source tree into "sqlite"
mkdir bld                     ;#  Build will occur in a sibling directory
cd bld                        ;#  Change to the build directory
../sqlite/configure           ;#  Run the configure script
make sqlite3                  ;#  Builds the "sqlite3" command-line tool
make sqlite3.c                ;#  Build the "amalgamation" source file
make sqldiff                  ;#  Builds the "sqldiff" command-line tool
# Makefile targets below this point require tcl-dev
make tclextension-install     ;#  Build and install the SQLite TCL extension
make devtest                  ;#  Run development tests
make releasetest              ;#  Run full release tests
make sqlite3_analyzer         ;#  Builds the "sqlite3_analyzer" tool
```



额外设置配置的内容

```
../sqlite/configure --enable-all --enable-debug CFLAGS='-O0 -g'
```



`CFLAGS='-O0 -g'`是一个用于设置编译选项的环境变量赋值语句。

1. `-O0`：
   * 这是优化级别选项。`-O0`表示不进行任何优化。在调试时通常使用这个选项，因为优化可能会改变代码的执行顺序、删除一些看似不必要的代码等，这会使得调试过程变得困难。不进行优化可以让代码按照原始的编写顺序执行，更易于跟踪和理解。
2. `-g`：
   * 这个选项用于生成调试信息。有了调试信息，调试器（如 `gdb`）可以在调试程序时显示变量名、行号、函数名等有用的信息，并且可以进行单步执行、查看变量值等操作。

总的来说，设置 `CFLAGS='-O0 -g'`通常是为了在编译代码时，确保生成的可执行文件易于调试，而不进行过度的优化。



CFLAGS 是一个环境变量，通常在使用编译工具（如 GCC、Clang 等）时用于指定编译选项。

它代表“C compiler flags”（C 编译器标志）。通过设置 CFLAGS，可以控制编译器如何处理源代码，包括优化级别、调试信息的生成、警告级别等。

例如：

* 设置优化级别：`CFLAGS='-O2'`表示使用中等程度的优化级别进行编译。
* 生成调试信息：`CFLAGS='-g'`用于生成调试信息，以便在调试器中进行代码调试。
* 开启特定的警告选项：`CFLAGS='-Wall -Wextra'`开启更多的警告信息，帮助开发者发现潜在的问题。

不同的项目可能会根据需要设置不同的 CFLAGS 值，以满足特定的编译要求。在 Makefile 或构建脚本中，经常会看到对 CFLAGS 的设置和使用。



这里可能遇到有关检测架构不匹配以及变异失败，很可能是我们的终端配置了CC有关的标签出现了那问题。





