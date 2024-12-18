# 1、SWiftUI更新UIKit 上的数据

## 实现场景： 我要通过SWiftUI上的一个列表的三个框框里面实现动画，并且他们之间有相互转换的场景动销

1. 涉及到动效播放， 这里使用了qvga 播放器
2. 因为qvga，目前是UIkit实现的第三方库， 而我们要实现这个功能，就需要将SWiftUI上的数据变化传递到UIkit中，这里就使用到了SWiftUI和UIKit之间的桥接Representable&#x20;
3. 因为有数据更新： 通过SWiftUI的数据更新到UIkit，因为SWiftUI是声明式，而UIkit常间的过程式，所以，需要使用Coordinantor来更新数据出发方法

#### 代码如下

{% code title="SwiftUI 端口" overflow="wrap" %}
```

class WARankDataViewModel: ObservableObject {
    @Published var lefts: [String] = []
    @Published var rightTops: [String] = []
    @Published var rightBottoms: [String] = []
    @Published var currentState: Bool = false

    private var vm: WAMainRoomViewModel
    private var timer: Timer?

    init(vm: WAMainRoomViewModel) {
        self.vm = vm
        setupInitialData()
        startTimer()
    }

    private func setupInitialData() {
        if let rankData = vm.rankData {
            lefts.append(contentsOf: rankData.wealthRatingingUtilizerPictureList ?? [])
            lefts.append(contentsOf: rankData.charmRatingingUtilizerPictureList ?? [])

            rightTops.append(contentsOf: rankData.charmRatingingUtilizerPictureList ?? [])
            rightTops.append(contentsOf: rankData.spaceRatingingBgList ?? [])

            rightBottoms.append(contentsOf: rankData.spaceRatingingBgList ?? [])
            rightBottoms.append(contentsOf: rankData.wealthRatingingUtilizerPictureList ?? [])
        }
    }

    private func startTimer() {
        if timer == nil {
            timer = Timer.scheduledTimer(withTimeInterval: 10, repeats: true) { [weak self] _ in
                self?.updateData()
            }
        }
    }

// 通过定时器更新数据
    private func updateData() {
        DispatchQueue.main.async { [weak self] in
            guard let self = self else { return }
            let tempLeft = self.lefts
            let tmpRightTop = self.rightTops
            let tmpRightBottom = self.rightBottoms
            
            self.lefts = Array(tmpRightTop)
            self.rightTops = Array(tmpRightBottom)
            self.rightBottoms = Array(tempLeft)

//            print("Updated data on main thread: \(self.lefts), \(self.rightTops), \(self.rightBottoms)")
//            print("Updated data on main thread: left first \(self.lefts.first!) ")
//            print("Updated data on main thread: top first \(self.rightTops.first!) ")
//            print("Updated data on main thread: bottom first \(self.rightBottoms.first!) ")
            self.currentState = !self.currentState
        }
    }

    deinit {
        timer?.invalidate()
        timer = nil
    }
}

struct WAKingKongView: View {
    
    @ObservedObject var vm: WAMainRoomViewModel
    @StateObject private var animateVM: WARankDataViewModel
    @State private var currentState: Bool = false // 主要通过这个来更新，因为数据可能会不变
    
    init(vm: WAMainRoomViewModel) {
        self.vm = vm
       _animateVM = StateObject(wrappedValue: WARankDataViewModel(vm: vm))
    }

    var body: some View {
        GeometryReader { proxy in
            HStack(spacing: 12~){
                WAHWDMP4PlayerView(sources: animateVM.lefts, currentState: animateVM.currentState)
                    .frame(width: (proxy.size.width - 12~)/2.0, height: proxy.size.height)
                    .background(Color.randomColor())
                    .cornerRadius(8~)
                VStack(spacing: 12~) {
                    WAHWDMP4PlayerView(
                        sources: animateVM.rightTops,
                        currentState: animateVM.currentState
                    )
                        .frame(width: (proxy.size.width - 12~)/2.0, height: (proxy.size.height - 12~)/2.0)
                        .background(Color.randomColor())
                        .cornerRadius(8~)
                    WAHWDMP4PlayerView(
                        sources: animateVM.rightBottoms,
                        currentState: animateVM.currentState
                    )
                        .frame(width: (proxy.size.width - 12~)/2.0, height: (proxy.size.height - 12~)/2.0)
                        .background(Color.randomColor())
                        .cornerRadius(8~)
                }
            }
        }
    }
}
```
{% endcode %}



{% code title="UIkit端" overflow="wrap" %}
```
//
//  HWDMP4PlayerController.swift
//  WAAW
//
//  Created by waaw on 18/12/2024.
//


// HWDMP4PlayerWrapper.swift
import SwiftUI
import QGVAPlayer
import SnapKit

class WAHWDMP4PlayerOriginView: UIView, HWDMP4PlayDelegate {
    // 假设VAPView是你要展示的view
    var vapView: UIView!
    var currentConfig:QGVAPConfigModel?
    var extraInfo : [String: String] = [:]
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        
        
        // 创建并添加VAPView到控制器的view中
        vapView = UIView(frame: self.bounds)
        self.addSubview(vapView)
        vapView.snp.makeConstraints { make in
            make.edges.equalToSuperview()
        }
        
        // 设置自己为委托
      
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    // 实现HWDMP4PlayDelegate的方法
    func shouldStartPlayMP4(container: UIView, config: QGVAPConfigModel) -> Bool {
        self.currentConfig = config;
        return true
    }
    
    func content(forVapTag tag: String!, resource info: QGVAPSourceInfo!) -> String! {
        let str = extraInfo[tag] ?? ""
        return str
    }
    
    func loadVapImage(
        withURL urlStr: String!,
        context: [AnyHashable : Any]!,
        completion completionBlock: VAPImageCompletionBlock!
    ) {
        guard let url = URL(string: urlStr) else {
            // Handle invalid URL
            completionBlock(nil, NSError(domain: "Invalid URL", code: -1, userInfo: nil), urlStr)
            return
        }

        Task {
            do {
                let (data, response) = try await URLSession.shared.data(from: url)
                
                guard let httpResponse = response as? HTTPURLResponse,
                      (200...299).contains(httpResponse.statusCode) else {
                    throw NSError(domain: "Failed to load image", code: -1, userInfo: nil)
                }
                
                if let image = UIImage(data: data) {
                    DispatchQueue.main.async {
                        completionBlock(image, nil, urlStr)
                    }
                } else {
                    throw NSError(domain: "Failed to create image from data", code: -1, userInfo: nil)
                }
            } catch {
                DispatchQueue.main.async {
                    completionBlock(nil, error, urlStr)
                }
            }
        }
    }
    
    func viewDidPlayMP4(at frame: QGMP4AnimatedImageFrame!, view container: UIView!) {
        if frame.frameIndex == 0 {
            vapView.pauseHWDMP4()
            DispatchQueue.main.asyncAfter(deadline: .now() + 5) { [self] in
                vapView.resumeHWDMP4()
            }
            return
        }
        
//        if let config = self.currentConfig {
//            if frame.frameIndex == config.info.framesCount - 1 {
//                vapView.pauseHWDMP4()
//            }
//        }
    }
    
    func updateSources(sources: [String], currentState: Bool) {
//        print("lt -- 更新 source \(sources)")
        vapView.stopHWDMP4()
        
//        let str = extraInfo[tag] ?? ""
        
        var innerExgtrainfo: [String: String] = [:]
        let extraList = ["CharmTop1profile", "CharmTop2profile", "CharmTop3profile","WealthTop1profile", "WealthTop2profile", "WealthTop3profile"]
        for (index, value) in extraList.enumerated() {
            innerExgtrainfo[value] = sources[index]
        }
        extraInfo = innerExgtrainfo
        let resouce = Bundle.main.resourcePath!.appending("/charm.mp4")
        vapView.playHWDMP4(resouce, repeatCount: 0, delegate: self)
    }
}

struct WAHWDMP4PlayerView: UIViewRepresentable {
    typealias UIViewType = WAHWDMP4PlayerOriginView

    var sources: [String]
    var currentState: Bool = false

    func updateUIView(_ uiView: WAHWDMP4PlayerOriginView, context: Context) {
        // 当绑定的 `sources` 发生变化时，这个方法会被调用
        if !sources.isEmpty {
            print("lt -- update source")
            uiView.updateSources(sources: sources, currentState: currentState)
        }
    }

    func makeUIView(context: Context) -> WAHWDMP4PlayerOriginView {
        let playerView = WAHWDMP4PlayerOriginView()
        return playerView
    }

    func makeCoordinator() -> Coordinator {
        Coordinator(self)
    }

// 通过Coordiantor 来管理管理 更新代码， 主要绑定的sources, currentSatate 发生变化，就会之心updateUIView 这个方法
    class Coordinator {
        private var parent: WAHWDMP4PlayerView

        init(_ parent: WAHWDMP4PlayerView) {
            self.parent = parent
        }

        // 如果你需要处理事件或其他逻辑，可以在这里添加方法
    }
}


1、实现有关播放器的代理
2、实现Coordinator来，因为数据的变化而出发更新
```
{% endcode %}
