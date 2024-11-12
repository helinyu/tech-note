# SCStreamConfiguration

`SCStreamConfiguration`类是Apple屏幕捕捉API的一部分，用于在macOS上配置屏幕录制和流媒体。该类的每个属性用于自定义屏幕捕获输出的不同方面，如分辨率、帧率、格式及特效。

以下是`SCStreamConfiguration`中各字段的详细解释：

#### 基础属性

* **width (Int)**：设置流的输出宽度（像素），默认为1920。
* **height (Int)**：设置流的输出高度（像素），默认为1080。
* **minimumFrameInterval (CMTime)**：指定帧更新的最小时间间隔（秒），默认值为1/60，表示最多60帧/秒。设置为`kCMTimeZero`则使用显示器的原生刷新率。
* **pixelFormat (OSType)**：指定输出的像素格式。支持的格式包括：
  * `BGRA`: ARGB8888，小端序打包。
  * `l10r`: ARGB2101010，小端序打包。
  * `420v`和`420f`: YCbCr 4:2:0，分别是“视频范围”和“完整范围”选项。
  * `xf44`: YCbCr10 4:4:4，完整范围。
  * `RGhA`: 64位RGBA，半精度浮点数。
* **scalesToFit (Bool)**：确定输出是否缩放以适应指定的宽度和高度。用于独立窗口捕获，`true`表示既可放大也可缩小，`false`仅允许缩小。

#### 长宽比与光标设置

* **preservesAspectRatio (Bool, macOS 14.0)**：启用时保持源画面的长宽比，默认启用。
* **streamName (String?, macOS 14.0)**：允许设置自定义流名称。
* **showsCursor (Bool)**：决定光标是否在流中可见，默认值为`true`。
* **showMouseClicks (Bool, macOS 15.0)**：如果为`true`，在点击时在光标周围显示一个圆圈，仅在`pixelFormat`设置为`BGRA`时有效。

#### 颜色和矩形

* **backgroundColor (CGColor)**：设置流的背景颜色，默认透明。
* **sourceRect (CGRect)**：指定要捕获的帧的子矩形，以显示的逻辑坐标系中的点为单位。默认情况下捕获整个显示器。
* **destinationRect (CGRect)**：指定输出缓冲区的子矩形，默认覆盖整个输出表面。

#### 队列和颜色设置

* **queueDepth (Int)**：指定缓冲队列中的帧数，默认为8帧。较大的值使用更多内存，但有助于帧处理。
* **colorMatrix (CFString)**：决定YCbCr转换矩阵，与`420v`和`420f`格式相关。
* **colorSpaceName (CFString)**：设置输出缓冲区的颜色空间，默认为显示器的颜色空间。

#### 音频属性

* **capturesAudio (Bool, macOS 13.0)**：启用音频捕获，默认为`false`。
* **sampleRate (Int, macOS 13.0)**：指定音频采样率，默认为48000 Hz。
* **channelCount (Int, macOS 13.0)**：设置音频通道数量，默认为双声道。
* **excludesCurrentProcessAudio (Bool, macOS 13.0)**：当为`true`时，排除当前进程的音频。

#### 其他显示选项

* **ignoreShadowsDisplay (Bool, macOS 14.0)** 和 **ignoreShadowsSingleWindow (Bool, macOS 14.0)**：启用时，在显示或单窗口捕获时忽略阴影。
* **captureResolution (SCCaptureResolutionType, macOS 14.0)**：允许选择“自动”、“最佳”和“标称”分辨率。
* **capturesShadowsOnly (Bool, macOS 14.0)**：启用时，仅捕获窗口的阴影。
* **shouldBeOpaque (Bool, macOS 14.0)**：当为`true`时，将窗口的部分透明区域替换为白色背景，使输出图像完全不透明。

#### 全局剪辑和隐私警告设置

* **ignoreGlobalClipDisplay (Bool, macOS 14.0)** 和 **ignoreGlobalClipSingleWindow (Bool, macOS 14.0)**：启用时，忽略显示或窗口剪辑，用于捕获屏幕外的区域。
* **presenterOverlayPrivacyAlertSetting (SCPresenterOverlayAlertSetting, macOS 14.0)**：控制使用演示者叠加时的隐私警告，默认为`SCPresenterOverlayAlertSettingSystem`。

#### 子窗口和麦克风设置

* **includeChildWindows (Bool, macOS 14.2)**：启用时，在显示边界捕获中包括子窗口。
* **captureMicrophone (Bool, macOS 15.0)**：启用麦克风捕获。
* **microphoneCaptureDeviceID (String?, macOS 15.0)**：指定用于捕获的麦克风设备ID。如果为`nil`，则使用默认系统麦克风。

#### 动态范围和预设

* **captureDynamicRange (SCCaptureDynamicRange, macOS 15.0)**：设置动态范围选项，如`SDR`、`HDRLocalDisplay`和`HDRCanonicalDisplay`。仅Apple Silicon设备支持HDR。
* **streamConfigurationWithPreset (Preset)**：便捷初始化器，返回具有指定预设建议的`SCStreamConfiguration`，帮助快速配置流。
