# NSUserActivity

`NSUserActivity` 是 iOS 和 macOS 中用于表示和管理用户活动的类。它常用于应用之间的跨设备操作（如 Handoff）和深度链接（如 Siri 建议和 Spotlight 搜索）的集成。通过 `NSUserActivity`，应用可以保存用户正在进行的任务状态，并在不同设备或会话之间继续执行这些任务。

#### 主要功能

1. **Handoff**：通过 Handoff 功能，用户可以在一台设备上开始任务，并无缝地在另一台设备上继续。例如，在 iPhone 上浏览网页并将其转移到 Mac 上继续浏览。
2. **Universal Links**：允许应用通过 URL 直接打开特定内容，同时保持应用内的状态。
3. **Siri Suggestions**：`NSUserActivity` 可以用来告诉 Siri 你的应用可以执行的操作，Siri 会根据用户的行为建议这些操作。
4. **Spotlight 搜索**：应用可以使用 `NSUserActivity` 将内容暴露给 Spotlight，这样用户可以在系统搜索中直接找到并启动应用的相关页面或功能。

#### 使用示例

通常，您会为每个具体的活动创建一个 `NSUserActivity` 实例，并设置其 `activityType` 和关联的元数据。

```objc
// 创建一个 NSUserActivity 实例
NSUserActivity *activity = [[NSUserActivity alloc] initWithActivityType:@"com.yourapp.viewingPage"];

// 设置与活动相关的信息
activity.title = @"View Article";
activity.userInfo = @{@"articleID" : @12345}; // 可以保存相关的自定义数据

// 添加深度链接信息
activity.webpageURL = [NSURL URLWithString:@"https://yourapp.com/articles/12345"];

// 设置活动的可继续性
activity.eligibleForHandoff = YES;
activity.eligibleForSearch = YES;
activity.eligibleForPublicIndexing = YES;

// 成为第一响应者
[self setUserActivity:activity];
```

#### 处理 Handoff

当用户在另一设备上继续活动时，系统会调用 `application:continueUserActivity:restorationHandler:` 来恢复状态：

```objc
- (BOOL)application:(UIApplication *)application
    continueUserActivity:(NSUserActivity *)userActivity
    restorationHandler:(void (^)(NSArray *restorableObjects))restorationHandler {
    
    if ([userActivity.activityType isEqualToString:@"com.yourapp.viewingPage"]) {
        // 恢复用户正在查看的文章
        NSString *articleID = userActivity.userInfo[@"articleID"];
        [self openArticleWithID:articleID];
        return YES;
    }
    
    return NO;
}
```

#### 常用属性

* `activityType`：标识该活动的类型，通常使用唯一字符串。
* `userInfo`：可以包含一些应用自定义的数据。
* `webpageURL`：与活动相关联的网页链接。
* `eligibleForHandoff`、`eligibleForSearch` 等：定义该活动是否可以用于 Handoff、Spotlight 搜索等。

这使得 `NSUserActivity` 成为在应用之间保持用户上下文、状态同步的关键组件。
