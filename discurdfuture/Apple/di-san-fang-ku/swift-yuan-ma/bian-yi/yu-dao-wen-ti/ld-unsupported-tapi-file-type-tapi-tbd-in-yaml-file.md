# ld: unsupported tapi file type '!tapi-tbd' in YAML file

{% code overflow="wrap" %}
```
CMake Error at /usr/local/Cellar/cmake/3.30.5/share/cmake/Modules/CMakeTestCCompiler.cmake:67 (message):
  The C compiler

    "/Users/helinyu/workspace/GitHub/space_swift/build/Ninja-DebugAssert/llvm-macosx-x86_64/bin/clang"

  is not able to compile a simple test program.

  It fails with the following output:

    Change Dir: '/Users/helinyu/workspace/GitHub/space_swift/build/Ninja-DebugAssert/llvm-macosx-x86_64/tools/clang/runtime/compiler-rt-bins/CMakeFiles/CMakeScratch/TryCompile-BsCvNH'

    Run Build Command(s): /opt/anaconda3/bin/ninja -v cmTC_bca1e
    [1/2][ 50%][0.694s] /Users/helinyu/workspace/GitHub/space_swift/build/Ninja-DebugAssert/llvm-macosx-x86_64/bin/clang   -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX15.0.sdk -mmacosx-version-min=13.0 -MD -MT CMakeFiles/cmTC_bca1e.dir/testCCompiler.c.o -MF CMakeFiles/cmTC_bca1e.dir/testCCompiler.c.o.d -o CMakeFiles/cmTC_bca1e.dir/testCCompiler.c.o -c /Users/helinyu/workspace/GitHub/space_swift/build/Ninja-DebugAssert/llvm-macosx-x86_64/tools/clang/runtime/compiler-rt-bins/CMakeFiles/CMakeScratch/TryCompile-BsCvNH/testCCompiler.c
    [2/2][100%][2.376s] : && /Users/helinyu/workspace/GitHub/space_swift/build/Ninja-DebugAssert/llvm-macosx-x86_64/bin/clang -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX15.0.sdk -mmacosx-version-min=13.0 -Wl,-search_paths_first -Wl,-headerpad_max_install_names -L/usr/local/opt/icu4c/lib CMakeFiles/cmTC_bca1e.dir/testCCompiler.c.o -o cmTC_bca1e   && :
    FAILED: cmTC_bca1e
    : && /Users/helinyu/workspace/GitHub/space_swift/build/Ninja-DebugAssert/llvm-macosx-x86_64/bin/clang -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX15.0.sdk -mmacosx-version-min=13.0 -Wl,-search_paths_first -Wl,-headerpad_max_install_names -L/usr/local/opt/icu4c/lib CMakeFiles/cmTC_bca1e.dir/testCCompiler.c.o -o cmTC_bca1e   && :
    ld: unsupported tapi file type '!tapi-tbd' in YAML file '/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX15.0.sdk/usr/lib/libSystem.tbd' for architecture x86_64
    clang: error: linker command failed with exit code 1 (use -v to see invocation)
    ninja: build stopped: subcommand failed.





  CMake will not be able to correctly generate this project.
Call Stack (most recent call first):
  CMakeLists.txt:14 (project)
```
{% endcode %}

遇到 `ld: unsupported tapi file type '!tapi-tbd'` 错误通常是由于与链接器（`ld`）或 Xcode SDK 相关的问题。以下是一些解决该问题的步骤和建议：



#### 0. <mark style="color:red;">很可能安装了conda —— 我的就是这个原因</mark>

暂时先去掉conda的 环境，很坑你conda的内容和xcode的工具冲突了

#### 1. 更新 Xcode 和 Command Line Tools

确保你的 Xcode 和 Command Line Tools 是最新版本。可以通过 Mac App Store 更新 Xcode，使用以下命令更新 Command Line Tools：

```bash
xcode-select --install
```

#### 2. 检查 Xcode 的命令行工具路径

确保 Xcode 的命令行工具路径是正确的。可以通过以下命令查看和设置：

```bash
xcode-select -p
```

如果路径不正确，可以使用以下命令设置：

```bash
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

#### 3. 确保 SDK 文件有效

检查 `/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/` 目录下的 SDK 文件。确保 `MacOSX15.0.sdk` 存在并且没有损坏。可以尝试重新安装 Xcode 或恢复 SDK 文件。

#### 4. 清理构建缓存

清理构建缓存可能会解决问题。你可以尝试以下步骤：

```bash
# 清理 CMake 缓存
rm -rf CMakeCache.txt CMakeFiles/
# 清理构建目录
rm -rf /Users/helinyu/workspace/GitHub/space_swift/build
```

#### 5. 使用不同的 SDK 版本

如果问题依然存在，考虑使用不同版本的 SDK。可以在终端中查看已安装的 SDK：

```bash
xcodebuild -showsdks
```

如果有其他版本的 macOS SDK（如 `MacOSX14.0.sdk`），可以在 CMake 配置中指定使用不同的 SDK：

```bash
cmake -DCMAKE_OSX_SYSROOT=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX14.0.sdk ..
```

#### 6. 使用其他构建工具

如果问题仍然存在，可以尝试使用其他构建工具，如 `make` 或 `ninja`。例如，使用 `ninja` 时，可以在 CMake 中指定：

```bash
cmake -G Ninja ..
```

#### 7. 检查环境变量

确保没有其他环境变量（如 `CC` 和 `CXX`）影响编译过程。可以通过以下命令检查：

```bash
echo $CC
echo $CXX
```

如果有设置，尝试取消它们并重新运行 CMake。



####

