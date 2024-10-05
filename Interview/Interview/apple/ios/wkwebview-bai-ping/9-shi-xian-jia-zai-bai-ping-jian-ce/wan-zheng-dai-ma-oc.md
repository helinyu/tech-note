# 完整代码(oc)

<pre><code>typedef NS_ENUM(NSUInteger,webviewLoadingStatus) {
    
    WebViewNormalStatus = 0, //正常
<strong>    
</strong>    WebViewErrorStatus, //白屏
    
    WebViewPendStatus, //待决
};


// 判断是否白屏
- (void)judgeLoadingStatus:(WKWebview *)webview  withBlock:(void (^)(webviewLoadingStatus status))completionBlock{
    webviewLoadingStatus __block status = WebViewPendStatus;
    if (@available(iOS 11.0, *)) {
        if (webview &#x26;&#x26; [webview isKindOfClass:[WKWebView class]]) {
            
            CGFloat statusBarHeight =  [[UIApplication sharedApplication] statusBarFrame].size.height; //状态栏高度
            CGFloat navigationHeight = webview.viewController.navigationController.navigationBar.frame.size.height; //导航栏高度
            WKSnapshotConfiguration *shotConfiguration = [[WKSnapshotConfiguration alloc] init];
            shotConfiguration.rect = CGRectMake(0, statusBarHeight + navigationHeight, webview.bounds.size.width, (webview.bounds.size.height - navigationHeight - statusBarHeight)); //仅截图检测导航栏以下部分内容
            [webview takeSnapshotWithConfiguration:shotConfiguration completionHandler:^(UIImage * _Nullable snapshotImage, NSError * _Nullable error) {
                if (snapshotImage) {
                    CGImageRef imageRef = snapshotImage.CGImage;
                    UIImage * scaleImage = [self scaleImage:snapshotImage];
                    BOOL isWhiteScreen = [self searchEveryPixel:scaleImage];
                    if (isWhiteScreen) {
                       status = WebViewErrorStatus;
                    }else{
                       status = WebViewNormalStatus;
                    }
                }
                if (completionBlock) {
                    completionBlock(status);
                }
            }];
        }
    }
}

// 遍历像素点 白色像素占比大于95%认定为白屏
- (BOOL)searchEveryPixel:(UIImage *)image {
    CGImageRef cgImage = [image CGImage];
    size_t width = CGImageGetWidth(cgImage);
    size_t height = CGImageGetHeight(cgImage);
    size_t bytesPerRow = CGImageGetBytesPerRow(cgImage); //每个像素点包含r g b a 四个字节
    size_t bitsPerPixel = CGImageGetBitsPerPixel(cgImage);
    
    CGDataProviderRef dataProvider = CGImageGetDataProvider(cgImage);
    CFDataRef data = CGDataProviderCopyData(dataProvider);
    UInt8 * buffer = (UInt8*)CFDataGetBytePtr(data);
    
    int whiteCount = 0;
    int totalCount = 0;
    
    for (int j = 0; j &#x3C; height; j ++ ) {
        for (int i = 0; i &#x3C; width; i ++) {
            UInt8 * pt = buffer + j * bytesPerRow + i * (bitsPerPixel / 8);
            UInt8 red   = * pt;
            UInt8 green = *(pt + 1);
            UInt8 blue  = *(pt + 2);
//            UInt8 alpha = *(pt + 3);
        
            totalCount ++;
            if (red == 255 &#x26;&#x26; green == 255 &#x26;&#x26; blue == 255) {
                whiteCount ++;
            }
        }
    }
    float proportion = (float)whiteCount / totalCount ;
    NSLog(@"当前像素点数：%d,白色像素点数:%d , 占比: %f",totalCount , whiteCount , proportion );
    if (proportion > 0.95) {
        return YES;
    }else{
        return NO;
    }
}

//缩放图片
- (UIImage *)scaleImage: (UIImage *)image {
    CGFloat scale = 0.2;
    CGSize newsize;
    newsize.width = floor(image.size.width * scale);
    newsize.height = floor(image.size.height * scale);
    if (@available(iOS 10.0, *)) {
        UIGraphicsImageRenderer * renderer = [[UIGraphicsImageRenderer alloc] initWithSize:newsize];
          return [renderer imageWithActions:^(UIGraphicsImageRendererContext * _Nonnull rendererContext) {
                        [image drawInRect:CGRectMake(0, 0, newsize.width, newsize.height)];
                 }];
    }else{
        return image;
    }
}

</code></pre>
