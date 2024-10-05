# 完整代码(swift)

```
import UIKit
import WebKit

/// 检查 Web 是否白屏
extension WKWebView {
    enum WebLoadingStatus{
        case normal
        case error
    }
    
    func judgeLoadingStatus(webView: WKWebView?, completion: ((_ status: WebLoadingStatus) -> Void)?) {
        
        if #available(iOS 11.0, *) {
            guard let webView = webView else {
                return
            }
            
            let window = UIApplication.shared.keyWindow
            guard let window = window else {
                return
            }
            
            let webViewRect = webView.convert(webView.bounds, to: window)
            
            let shotConfiguration = WKSnapshotConfiguration()
            shotConfiguration.rect = CGRect(x: webViewRect.origin.x, y: webViewRect.origin.y, width: webViewRect.size.width, height: webViewRect.size.height)
            
            webView.takeSnapshot(with: shotConfiguration) { [weak self] (image, error) in
                guard let self = self, let image = image else {
                    return
                }
                
                let scaleImage = self.scaleImage(image: image)
                let isWhiteScreen = self.searchEveryPixel(image: scaleImage)
                
                if isWhiteScreen {
                    completion?(.error)
                } else {
                    completion?(.normal)
                }
            }
        }
    }
    
    /// 遍历像素点，判断白色像素是否占比大于 95%
    /// - Parameter image: 图片
    /// - Returns: 占比
    private func searchEveryPixel(image: UIImage) -> Bool {
        let cgImage = image.cgImage
        let width: size_t = cgImage?.width ?? 0
        let height: size_t = cgImage?.height ?? 0
        
        let dataProvider = cgImage?.dataProvider
        let data = dataProvider?.data
        let buffer: UnsafePointer<UInt8> = CFDataGetBytePtr(data)
        
        var whiteCount = 0
        var totalCount = 0
        
        for x in 0 ..< height {
            for y in 0 ..< width {
                
                let point = CGPoint(x: x, y: y)
                let pixelInfo: Int = (width * Int(point.y)) + Int(point.x) * 4
                
                let red = CGFloat(buffer[pixelInfo])
                let green = CGFloat(buffer[pixelInfo + 1])
                let blue = CGFloat(buffer[pixelInfo + 2])
                
                if red == 255.0 && green == 255.0 && blue == 255.0 {
                    whiteCount += 1
                }
                
                totalCount += 1
            }
        }
        
        let proportion: CGFloat = CGFloat(whiteCount / totalCount)
        
        if proportion > 0.95 {
            return true
        } else {
            return false
        }
    }
    
    /// 缩放图片
    /// 为了提升检测性能，考虑将快照缩放至1/5，减少像素点总数，从而加快遍历速度
    /// - Parameter image: 原始图片
    /// - Returns: 缩放后图片
    private func scaleImage(image: UIImage) -> UIImage {
        let scale = 0.2
        // 缩略图的尺寸在原图宽高 * 缩放系数后可能不是整数，在布置画布重绘时默认向上取整，这就造成画布比实际缩略图大
        // 造成不准确，所以此处选择 向下取整
        let newSize = CGSize(width: floor(image.size.width * scale), height: floor(image.size.height * scale))
        
        if #available(iOS 13.0, *) {
            let renderer = UIGraphicsImageRenderer(size: newSize)
            
            renderer.image { rendererContext in
                return image.draw(in: CGRect(x: 0, y: 0, width: newSize.width, height: newSize.height))
            }
        }
        return image
    }
}
```
