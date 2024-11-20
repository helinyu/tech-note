# iOS真机测试步骤

让 iOS 应用进行真机测试的步骤如下：

***

#### **1. 开发者账号准备**

* 确保你拥有一个 Apple 开发者账号（需要付费订阅 Apple Developer Program）。
* 登录 [Apple Developer 网站](https://developer.apple.com/) 以管理相关证书和设备。

***

#### **2. 配置开发环境**

1. **Xcode 安装**
   * 下载并安装最新版的 Xcode。
   * 打开 Xcode，确保已登录开发者账号（`Preferences` -> `Accounts` 中添加 Apple ID）。
2. **连接测试设备**
   * 使用 USB 数据线将 iOS 设备连接到电脑。
   * 确保设备已在信任状态，第一次连接需要在设备上点击“信任此电脑”。

***

#### **3. 创建证书和配置文件**

1. **生成开发证书**
   * 登录 [Apple Developer](https://developer.apple.com/) 网站。
   * 导航至 **Certificates, Identifiers & Profiles** -> **Certificates**。
   * 生成一个 iOS 开发者证书（Development Certificate）。
2. **添加设备**
   * 在 **Devices** 部分添加你的测试设备（需要设备的 UDID）。
   * 你可以通过以下方式获取设备 UDID：
     * 在 iTunes 或 Finder 中查看设备信息。
     * 在 Xcode 的设备列表中找到设备右键复制 UDID。
3. **创建 App ID**
   * 在 **Identifiers** 中创建一个对应应用的 App ID。
4. **创建配置文件（Provisioning Profile）**
   * 在 **Profiles** 中创建一个 iOS Development 配置文件，选择对应的 App ID、开发证书和设备。

***

#### **4. Xcode 配置项目**

1. 打开你的 Xcode 项目，选择目标项目 **Target**。
2. 在 **Signing & Capabilities** 页面：
   * 勾选 **Automatically manage signing**。
   * 选择你的开发者团队（Team）。
   * Xcode 会自动下载并使用对应的配置文件。

***

#### **5. 部署到真机**

1. 在 Xcode 左上角选择目标设备（已连接的 iOS 设备）。
2. 点击 **Run（运行）** 按钮，Xcode 会编译并安装应用到设备上。
3. 如果是第一次安装，可能会弹出“未信任的开发者”提示：
   * 在设备上打开 **设置 -> 通用 -> VPN 与设备管理**。
   * 找到对应的开发者证书，点击“信任”。

***

#### **6. 测试应用**

* 在设备上启动应用，测试其功能和性能。
* 如果需要多台设备测试，可以重复添加设备步骤。

***

#### **7. 使用 TestFlight 进行分发（可选）**

* 如果需要团队或远程测试，可以使用 TestFlight 分发应用：
  1. 在 Xcode 中将应用打包为 Ad Hoc 或 App Store 分发。
  2. 上传至 App Store Connect。
  3. 邀请测试者进行测试。

完成这些步骤后，便可在真机上顺利测试你的 iOS 应用。
