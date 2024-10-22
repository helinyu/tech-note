# H.264 硬解码

H.264 硬解码是使用专用硬件来解码 H.264 视频流的一种方式，通常利用设备的 GPU 或其他视频解码器来实现。相较于软件解码，硬解码具有更高的效率和更低的能耗，非常适合需要实时处理或低延迟的应用场景。以下是有关 H.264 硬解码的一些详细信息：

#### H.264 概述

* **H.264 (AVC)**：是一种常用的视频压缩标准，广泛应用于视频流、蓝光光盘、视频会议等。
* **优点**：提供高压缩比和良好的视频质量，使其成为现代视频传输和存储的主流选择。

#### 硬解码的优势

1. **性能**：
   * 硬解码利用专用硬件（如 GPU 或视频解码器），可以在解码过程中显著提高性能，减少 CPU 的负担。
2. **能效**：
   * 硬件解码通常消耗更少的电力，这对移动设备（如智能手机、平板电脑）特别重要。
3. **低延迟**：
   * 硬解码可以实现低延迟的视频解码，适合实时应用，如视频通话和在线游戏。

#### 使用 VideoToolbox 进行 H.264 硬解码

使用 VideoToolbox.framework 进行 H.264 硬解码的基本步骤如下：

1. **创建解码会话**：
   * 使用 `VTDecompressionSessionCreate` 创建解码会话，并指定输出回调函数。
2. **设置解码参数**：
   * 提供编码的格式描述（如 SPS/PPS 数据），并设置解码会话的参数。
3. **提供压缩数据**：
   * 使用 `VTDecompressionSessionDecodeFrame` 方法将 H.264 压缩数据发送到解码会话。
4. **处理输出图像**：
   * 在输出回调中接收解码后的图像帧，进行进一步处理或渲染。

#### 示例代码

以下是使用 VideoToolbox 进行 H.264 硬解码的简单示例：

```objc
// 1. 创建解码会话
VTDecompressionSessionRef decompressionSession;
VTDecompressionOutputCallback callback = {
    .decompressionOutputCallback = outputCallback,
    .decompressionOutputRefCon = (__bridge void *)(self)
};

VTDecompressionSessionCreate(kCFAllocatorDefault, formatDescription, NULL, &callback, &decompressionSession);

// 2. 提供压缩数据
VTDecodeFrameFlags flags = 0;
CMTime presentationTimeStamp = CMTimeMake(0, 30); // 假设帧率为30 FPS
VTDecompressionSessionDecodeFrame(decompressionSession, sampleBuffer, flags, NULL, &presentationTimeStamp);
```

#### 注意事项

* 确保设备支持 H.264 硬解码，某些老旧设备可能不支持。
* 需要正确管理内存和资源，避免内存泄漏或性能问题。
* 对于不同的 H.264 流（例如，带有不同分辨率、帧率的流），需要相应地调整解码会话的参数。

H.264 硬解码是实现高效视频播放和处理的关键技术，如果你有更具体的应用场景或技术细节想了解，请随时告诉我！
