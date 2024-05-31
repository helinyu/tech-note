---
description: 流配置
---

# SCStreamConfiguration

```

@available(macOS 12.3, *)
open class SCStreamConfiguration : NSObject {

// 《1》Specifying dimensions 指定尺寸

    open var width: Int
    open var height: Int
    open var scalesToFit: Bool // scale填充
    open var sourceRect: CGRect // 源位置大小，如果没有设置，将会展示原始的逻辑坐标系统显示
    open var destinationRect: CGRect // 目标的位置大小
    //是否保持原来流的像素数据，默认是保留的
    @available(macOS 14.0, *)
    open var preservesAspectRatio: Bool

// 《2》Configuring colors配置颜色
    open var pixelFormat: OSType // 支持的像素类型BGRA、l10r、420v、420f https://developer.apple.com/documentation/coregraphics/1455170-cgdisplaystreamcreate
    unowned(unsafe) open var colorMatrix: CFString  // 用于指定输出的颜色矩阵，只在420v or 420f格式 https://developer.apple.com/documentation/coregraphics/quartz_display_services/display_stream_ycbcr_to_rgb_conversion_matrix_options
    unowned(unsafe) open var colorSpaceName: CFString //指定颜色空间的输出缓存，如果没有指定就是和显示的一样，值可查 https://developer.apple.com/documentation/coregraphics/cgcolorspace/color_space_names.
    unowned(unsafe) open var backgroundColor: CGColor // 背景颜色，默认是透明的

// 《3》Configuring captured elements 配置捕获因素
    open var showsCursor: Bool // 显示游标 ，默认是可见的
    @available(macOS 14.0, *)
    open var shouldBeOpaque: Bool // 是否为不透明，设置就位填充的白色
    @available(macOS 14.0, *)
    open var capturesShadowsOnly: Bool // 只是捕获window的阴影
    @available(macOS 14.0, *)
    open var ignoreShadowsDisplay: Bool // 忽略阴影的展示
    @available(macOS 14.0, *)
    open var ignoreShadowsSingleWindow: Bool // 忽略单个窗口的阴影
        @available(macOS 14.0, *)
    open var ignoreGlobalClipDisplay: Bool // 忽略全局剪切的显示
    @available(macOS 14.0, *)
    open var ignoreGlobalClipSingleWindow: Bool // 忽略单个阴影剪切

// 《4》Configuring captured frames 配置捕获帧
    open var queueDepth: Int // 指定在队列中的帧数，默认是8帧，指定更多的帧消耗内存更多；但是可以允许您在不停止显示流的情况下处理帧数据，并且不应超过8帧
    open var minimumFrameInterval: CMTime // 指定更新帧的最小间隔，允许你接收更新额速率；，默认是0，以为不容忍
    @available(macOS 14.0, *)
    open var captureResolution: SCCaptureResolutionType // 捕获的分辨率 ，automatic, best, and nominal

    public enum SCCaptureResolutionType : Int, @unchecked Sendable {
            case automatic = 0 // 自动，根据网络等因素总选择分辨率
            case best = 1 // 最佳可用分辨率
            case nominal = 2 // 点：像素 = 1:1
        }

    
// 《5》Configuring audio 配置音频
    @available(macOS 13.0, *)
    open var capturesAudio: Bool // 是否捕获音频， 默认：false
    @available(macOS 13.0, *)
    open var sampleRate: Int // 音频采样率，默认是：48000
    @available(macOS 13.0, *)
    open var channelCount: Int // 频道数量，默认是2
    @available(macOS 13.0, *)
    open var excludesCurrentProcessAudio: Bool // 不包括当前的进程音频道， 默认是NO
 
// 《6》Identifying a stream 标识一个流
    @available(macOS 14.0, *)
    open var streamName: String? // 流名，用于标识流

// 《7》Notifying presenters 通知演示者
    @available(macOS 14.0, *)
    open var presenterOverlayPrivacyAlertSetting: SCPresenterOverlayAlertSetting // 隐私的设置，就是我们使用设备的时候的弹框，默认是SCPresenterOverlayAlertSettingSystem
    @available(macOS 14.0, *)
    public enum SCPresenterOverlayAlertSetting : Int, @unchecked Sendable {
        case system = 0 // 系统根据判断
        case never = 1 // 从来不
        case always = 2 // 总是
    }
    
// 《8》Instance Properties 实例属性
    @available(macOS 14.2, *)
    open var includeChildWindows: Bool // 是否包括子窗口，默认是：YES
}

```

