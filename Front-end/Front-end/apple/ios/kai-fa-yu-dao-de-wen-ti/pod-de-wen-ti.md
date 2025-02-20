# pod的问题



#### 1. pod install 出现错误NoMethodError - undefined method 'name' for an instance of Xcodeproj::Project::Object::PBXSourcesBuildPhase

这个错误通常发生在 `Podfile` 或者 `Podfile.lock` 与项目的 Xcode 配置存在不一致时，尤其是当 CocoaPods 与 Xcode 的版本不兼容或某个 pod 的配置出现问题时

删除.Podfile.lock ，然后重新 pod install安装第三方库。&#x20;



也有可能是网络的问题， 可以先将崩溃的那个pod注释掉，安装了其他的之后，在回来安装崩溃的pod。



