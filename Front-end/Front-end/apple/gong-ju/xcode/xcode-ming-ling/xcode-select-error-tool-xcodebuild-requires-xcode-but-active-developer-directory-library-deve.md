# xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Deve

xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance ERROR: command `['xcodebuild', '-version']` terminated with a non-zero exit status 1, aborting



这个错误提示你当前的开发环境配置有问题。具体来说，`xcode-select` 工具检测到你使用的是 `CommandLineTools` 的命令行工具路径，而某些命令（如 `xcodebuild`）需要完整安装的 Xcode。

以下是解决方法：

***

#### 方法一：安装完整的 Xcode

1. 打开 Mac App Store，搜索 **Xcode** 并下载安装。
2.  安装完成后，运行以下命令切换到 Xcode 的开发工具目录：

    ```bash
    sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
    ```
3.  检查是否切换成功：

    ```bash
    xcode-select -p
    ```

    输出应该是 `/Applications/Xcode.app/Contents/Developer`。
4.  测试 `xcodebuild` 是否正常工作：

    ```bash
    xcodebuild -version
    ```

    如果能输出 Xcode 版本信息，则表示问题解决。

***

#### 方法二：重新安装或修复命令行工具

如果不需要完整的 Xcode，可以尝试以下步骤：

1.  重新安装 Command Line Tools：

    ```bash
    xcode-select --install
    ```

    安装完成后，确认路径：

    ```bash
    xcode-select -p
    ```

    输出应为 `/Library/Developer/CommandLineTools`。
2.  检查 `xcodebuild`：

    ```bash
    xcodebuild -version
    ```

    如果仍然出错，说明某些操作确实需要完整的 Xcode，建议安装完整版本。

***

#### 方法三：确认是否有权限问题

1.  确保你有足够的权限访问开发工具：

    ```bash
    sudo xcode-select --reset
    ```
2. 再次测试命令。

***

#### 注意事项

* 如果你运行的是需要 `xcodebuild` 的软件或工具，比如某些 Python 库的编译工具，请确保 Xcode 已经安装。
* 安装 Xcode 后，记得打开 Xcode 并接受其许可证协议（首次使用时会提示）。
