# Sandbox: rsync.samba(16050) deny(1) file-write-create /xxx/Xcode/Derived

您遇到的 `Sandbox: rsync.samba deny(1)` 错误是由于应用在构建过程中尝试写入到沙盒限制不允许的目录。这通常发生在使用第三方库或框架时，涉及到打包资源文件或构建过程中的路径问题。

#### 解决方案

**1. 清理 DerivedData 目录**

Xcode 有时会在 `DerivedData` 目录中缓存不完整或错误的构建结果，清理该目录可以解决许多类似的问题。

步骤：

1. 打开 Xcode。
2. 在顶部菜单中选择 **Product > Clean Build Folder**（快捷键：`Shift + Command + K`）。
3. 如果问题仍然存在，手动删除 `DerivedData` 目录：
   *   运行以下命令清理：

       ```bash
       rm -rf ~/Library/Developer/Xcode/DerivedData
       ```
   * 或者在 Finder 中导航到 `~/Library/Developer/Xcode/DerivedData` 并删除所有内容。

***

**2. 检查项目路径权限**

确保您的项目路径和 `DerivedData` 目录都有写入权限：

1.  在终端中检查权限：

    ```bash
    ls -ld ~/Library/Developer/Xcode/DerivedData
    ```
2.  如果权限不足，可以修改权限：

    ```bash
    chmod -R u+w ~/Library/Developer/Xcode/DerivedData
    ```

***

**3. 修改构建路径**

可以尝试将构建路径移到其他位置：

1. 打开 Xcode。
2. 前往 **Xcode > Settings > Locations**。
3. 在 **Derived Data** 部分，点击 **Advanced**，选择一个新的目录（如项目根目录外的一个子目录）。

***

**4. 检查资源冲突**

根据错误信息，问题可能与 `Protobuf_Privacy.bundle` 有关：

1. 确认 `Protobuf` 框架的版本是否兼容。
2. 检查是否有多个版本的 `Protobuf.framework` 或重复的资源在被打包。
3. 如果可能，尝试重新安装或更新依赖项。

如果使用 CocoaPods，尝试更新或重新安装：

```bash
pod deintegrate
pod install
```

***

**5. 禁用沙盒限制（仅调试用途）**

如果上述方法未解决问题，可以尝试临时禁用沙盒限制：

1. 打开项目的 `.xcodeproj` 或 `.xcworkspace`。
2. 选择 **Edit Scheme**。
3.  找到 **Run** 配置，取消勾选 **Enable App Sandbox**。

    > **注意**：仅用于本地调试，不适用于生产环境。

***

**6. 更新 Xcode 和依赖**

确保使用的 Xcode 和依赖库是最新版本：

1. 更新 Xcode 到最新稳定版本。
2. 更新 `Protobuf` 框架的版本。

***

如果问题仍未解决，请提供以下信息：

* 使用的 Xcode 版本。
* 相关第三方库（如 `Protobuf`）的版本。
* 更完整的错误日志或构建设置。



### 解法：

在xcode中的build settings 中设置enable\_user 收缩，改设置为NO。&#x20;

