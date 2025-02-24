# pod的问题

## 1. pod install 出现错误NoMethodError - undefined method 'name' for an instance of Xcodeproj::Project::Object::PBXSourcesBuildPhase

1. 很可能 **库** 的版本不对
2. podfile.lock文件的影响，需要重新更新pod内容，要将pod相关的内容删除完，重新安装
   1. podfile.lock 文件锁死了，可以考虑删除
   2. rm -rf Podsrm Podfile.lockrm -rf \*.xcworkspacepod install ,, 以及打开.project.xcodej 文件， 删除和pod有关的文件。
3. ˙终端执行命令：

{% code overflow="wrap" %}
```
sed -i -e 's/build_phase.name/build_phase.display_name/g' "$(gem info xcodeproj --version 1.27.0  | grep 'Installed at:' | cut -d':' -f 2 | xargs)/gems/xcodeproj-1.27.0/lib/xcodeproj/project/object/file_system_synchronized_exception_set.rb" 
```
{% endcode %}



## 2. SDK does not contain 'libarclite' at the path '/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/arc/libarclite\_iphonesimulator.a'; try increasing the minimum deployment target

要设置最低的版本 , 可能有些库和有些版本匹配不上。

```
post_install do |installer|
    installer.generated_projects.each do |project|
        project.targets.each do |target|
            target.build_configurations.each do |config|
                config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '14.0'
            end
        end
    end
end
```

## 3. xcode16 不支持bitcode了

{% embed url="https://help.rongcloud.cn/t/topic/1241" %}

#### Podfile 文件中添加代码：

```
post_install do |installer|
  bitcode_strip_path = `xcrun --find bitcode_strip`.chop!
  
  def strip_bitcode_from_framework(bitcode_strip_path, framework_relative_path)
        framework_path = File.join(Dir.pwd, framework_relative_path)
        command = "#{bitcode_strip_path} #{framework_path} -r -o #{framework_path}"
        puts "Stripping bitcode: #{command}"
        system(command)
  end

  RongCloudIM_Frameworks = [
  "RongChatRoom",
  "RongContactCard",
  "RongCustomerService",
  "RongDiscussion",
  "RongIMKit",
  "RongIMLib",
  "RongIMLibCore",
  "RongLocation",
  "RongLocationKit",
  "RongPublicService",
  "RongSight",
  "RongSticker"
  ]

  RongCloudIM_Frameworks.each do |framework_name|
    framework_relative_path ="Pods/RongCloudIM/RongCloudIM/#{framework_name}.xcframework/ios-arm64_armv7/#{framework_name}.framework/#{framework_name}"
    strip_bitcode_from_framework(bitcode_strip_path, framework_relative_path)
  end
end
```
