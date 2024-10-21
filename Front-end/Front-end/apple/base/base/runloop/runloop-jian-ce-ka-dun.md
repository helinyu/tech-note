# Runloop检测卡顿

使用 `CFRunLoopObserver` 来监测 RunLoop 的状态是检测卡顿的有效方法。下面是一个示例，展示如何使用 `CFRunLoopObserver` 来监测 RunLoop 的运行情况，并记录任务的执行时间。

#### 示例代码

```objc
#import <Foundation/Foundation.h>
#import <CoreFoundation/CoreFoundation.h>

void RunLoopObserverCallback(CFRunLoopObserverRef observer, CFRunLoopActivity activity, void *info) {
    static CFTimeInterval lastTime = 0;
    CFTimeInterval currentTime = CFAbsoluteTimeGetCurrent();
    
    if (activity == kCFRunLoopBeforeWaiting) {
        // 进入等待状态前的回调
        CFTimeInterval deltaTime = currentTime - lastTime;
        if (deltaTime > 0.1) { // 如果超过100ms，则可能存在卡顿
            NSLog(@"Possible lag detected: %f seconds", deltaTime);
        }
    }
    
    // 更新最后执行时间
    lastTime = currentTime;
}

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // 创建一个 RunLoop Observer
        CFRunLoopObserverContext context = {0, NULL, NULL, NULL, NULL};
        CFRunLoopObserverRef observer = CFRunLoopObserverCreate(NULL, 
                                                                kCFRunLoopAllActivities, 
                                                                true, 
                                                                0, 
                                                                RunLoopObserverCallback, 
                                                                &context);
        
        // 将 Observer 添加到主 RunLoop
        CFRunLoopAddObserver(CFRunLoopGetCurrent(), observer, kCFRunLoopDefaultMode);
        
        // 开始 RunLoop
        CFRunLoopRun();
        
        // 释放资源
        CFRunLoopRemoveObserver(CFRunLoopGetCurrent(), observer, kCFRunLoopDefaultMode);
        CFRelease(observer);
    }
    return 0;
}
```

#### 代码说明

1. **创建 Observer**：
   * 使用 `CFRunLoopObserverCreate` 创建一个 RunLoop Observer。可以通过设置观察的活动类型（如 `kCFRunLoopAllActivities`）来监测 RunLoop 的所有活动。
2. **回调函数**：
   * 在回调函数 `RunLoopObserverCallback` 中，检查当前时间与上次记录的时间之间的差值。如果差值超过了设定的阈值（如 100 毫秒），则打印可能的卡顿信息。
3. **添加到 RunLoop**：
   * 使用 `CFRunLoopAddObserver` 将 Observer 添加到当前的 RunLoop 中。
4. **运行 RunLoop**：
   * 通过 `CFRunLoopRun` 启动 RunLoop，应用程序将持续运行并处理事件。
5. **释放资源**：
   * 在退出时，使用 `CFRunLoopRemoveObserver` 和 `CFRelease` 释放 Observer。

#### 注意事项

* 你可以根据具体需求调整时间阈值，以便更好地捕捉到应用中的卡顿情况。
* 在实际项目中，确保在合适的地方添加 Observer，并在适当的时机移除，以避免对性能的负担。
