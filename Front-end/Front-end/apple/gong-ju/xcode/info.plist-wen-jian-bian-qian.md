# info.plist文件变迁

<figure><img src="../../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

**从Xcode13开始，新建的工程不再要求使用配置文件（Info.plist、entitlements）。如果需要修改Xcode的配置，请直接在Xcode面板"target - Info - Custom iOS Target Properties"和"build settings"中设置**。

其实，早在Xcode13之前，“Custom iOS Target Properties”这个面板就有了，只是Xcode会自动同步“Cusutom iOS Target Properties”和Info.plist文件。而现在，Xcode13默认删除了Info.plist文件中的大部分属性，保留在“Cusutom iOS Target Properties”中。

**其实，info.plist并没有被“干掉”，打包时Xcode会自动生成Info.plist文件。包体内最终的Info.plist文件是由工程中的Custom iOS Target Properties、buildSetting 两者者合并生成的。**。

