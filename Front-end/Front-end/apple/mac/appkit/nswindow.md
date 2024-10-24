# NSWindow

```
- (void)center; // 这个哦那劲
- (void)makeKeyAndOrderFront:(nullable id)sender; // 这个还有聚焦
- (void)orderFront:(nullable id)sender;// 排序在谁的前面，如果nil表示最前面
- (void)orderBack:(nullable id)sender; // 后面
- (void)orderOut:(nullable id)sender; // 
- (void)orderWindow:(NSWindowOrderingMode)place relativeTo:(NSInteger)otherWin;
- (void)orderFrontRegardless; //用于将窗口强制显示到最前端，无论当前应用是否在活跃状态。
```
