---
description: 检查共享内容 —— 主要是共享对象
---

# \[共享内容对象]Inspecting shareable content

```
//  运行的程序
@available(macOS 12.3, *)
open class SCRunningApplication : NSObject {

// bundleID
    open var bundleIdentifier: String { get }

// 程序名
    open var applicationName: String { get }

    // 进程ID
    open var processID: pid_t { get }
}

// 窗口
@available(macOS 12.3, *)
open class SCWindow : NSObject {

// 窗口ID
    open var windowID: CGWindowID { get }

// 位置大小
    open var frame: CGRect { get }

// 标题
    open var title: String? { get }

    // 窗口层
    open var windowLayer: Int { get }

    // 拥有的程序 —— 应该是这个窗口是哪个程序的
    open var owningApplication: SCRunningApplication? { get }

    
// 这个窗口是否再屏幕上
    open var isOnScreen: Bool { get }

    
// 是否活跃
    @available(macOS 13.1, *)
    open var isActive: Bool { get }
}

//  显示设备的对象
@available(macOS 12.3, *)
open class SCDisplay : NSObject {
    open var displayID: CGDirectDisplayID { get }
    open var width: Int { get }
    open var height: Int { get }
    open var frame: CGRect { get }
}

```
