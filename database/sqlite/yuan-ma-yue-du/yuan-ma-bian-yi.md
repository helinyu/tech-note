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



这里可能遇到有关检测架构不匹配以及变异失败，很可能是我们的终端配置了CC有关的标签出现了那问题。



