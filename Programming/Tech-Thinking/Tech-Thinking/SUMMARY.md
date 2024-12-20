# Table of contents

* [REAdME](README.md)
* [技术点思考](ji-shu-dian-si-kao/README.md)
  * [内存管理](ji-shu-dian-si-kao/nei-cun-guan-li/README.md)
    * [内存管理进化史](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-guan-li-jin-hua-shi/README.md)
      * [分代垃圾回收vs垃圾回收](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-guan-li-jin-hua-shi/fen-dai-la-ji-hui-shou-vs-la-ji-hui-shou.md)
      * [引用计数vs垃圾回收](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-guan-li-jin-hua-shi/yin-yong-ji-shu-vs-la-ji-hui-shou.md)
    * [内存回收机制](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-hui-shou-ji-zhi/README.md)
      * [手动管理](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-hui-shou-ji-zhi/shou-dong-guan-li.md)
      * [垃圾回收](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-hui-shou-ji-zhi/la-ji-hui-shou/README.md)
        * [引用计数](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-hui-shou-ji-zhi/la-ji-hui-shou/yin-yong-ji-shu.md)
        * [基本内容](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-hui-shou-ji-zhi/la-ji-hui-shou/ji-ben-nei-rong.md)
        * [GC垃圾回收的实现方式](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-hui-shou-ji-zhi/la-ji-hui-shou/gc-la-ji-hui-shou-de-shi-xian-fang-shi.md)
    * [内存对齐(Memory Alignment)](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-dui-qi-memory-alignment/README.md)
      * [是什么？](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-dui-qi-memory-alignment/shi-shen-me.md)
      * [内存对齐是不是在所有的编程语言中都得有？](ji-shu-dian-si-kao/nei-cun-guan-li/nei-cun-dui-qi-memory-alignment/nei-cun-dui-qi-shi-bu-shi-zai-suo-you-de-bian-cheng-yu-yan-zhong-du-de-you.md)
    * [智能指针](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/README.md)
      * [现代语言与智能指针](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/xian-dai-yu-yan-yu-zhi-neng-zhi-zhen.md)
      * [C++](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/c++/README.md)
        * [std::unique\_ptr](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/c++/std-unique\_ptr.md)
        * [td::shared\_ptr、std::weak\_ptr](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/c++/td-shared\_ptr-std-weak\_ptr.md)
        * [删除器](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/c++/shan-chu-qi.md)
      * [Rust](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/rust/README.md)
        * [Box\<T>](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/rust/box-less-than-t-greater-than.md)
        * [Rc\<T> 和 RefCell\<T> 和Weak\<T>](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/rust/rct-he-refcellt-he-weakt.md)
        * [Arc\<T> 、RefCell\<T> 、weak\<T>](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/rust/arc-less-than-t-greater-than-refcell-less-than-t-greater-than-weak-less-than-t-greater-than.md)
        * [类比C++](ji-shu-dian-si-kao/nei-cun-guan-li/zhi-neng-zhi-zhen/rust/lei-bi-c++.md)
  * [编程范式](ji-shu-dian-si-kao/bian-cheng-fan-shi/README.md)
    * [面向对象编程（OOP）](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/README.md)
      * [优缺点](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/you-que-dian.md)
      * [类主要概念](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/README.md)
        * [类对象](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/lei-dui-xiang/README.md)
          * [OC](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/lei-dui-xiang/oc.md)
          * [C++](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/lei-dui-xiang/c++.md)
        * [三大特性](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/san-da-te-xing/README.md)
          * [多态](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/san-da-te-xing/duo-tai/README.md)
            * [是什么？](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/san-da-te-xing/duo-tai/shi-shen-me.md)
            * [C++上的多态](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/san-da-te-xing/duo-tai/c++-shang-de-duo-tai.md)
            * [OC中的多态](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/san-da-te-xing/duo-tai/oc-zhong-de-duo-tai.md)
            * [C++ vs OC](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/lei-zhu-yao-gai-nian/san-da-te-xing/duo-tai/c++-vs-oc.md)
      * [Page](ji-shu-dian-si-kao/bian-cheng-fan-shi/mian-xiang-dui-xiang-bian-cheng-oop/page.md)
  * [函数/方法](ji-shu-dian-si-kao/han-shu-fang-fa/README.md)
    * [重载](ji-shu-dian-si-kao/han-shu-fang-fa/zhong-zai.md)
    * [方法重写](ji-shu-dian-si-kao/han-shu-fang-fa/fang-fa-zhong-xie/README.md)
      * [函数没有重写](ji-shu-dian-si-kao/han-shu-fang-fa/fang-fa-zhong-xie/han-shu-mei-you-zhong-xie.md)
    * [重写vs重载](ji-shu-dian-si-kao/han-shu-fang-fa/zhong-xie-vs-zhong-zai.md)
  * [Page 1](ji-shu-dian-si-kao/page-1.md)
* [编程范式](bian-cheng-fan-shi/README.md)
  * [编程范式](bian-cheng-fan-shi/bian-cheng-fan-shi/README.md)
    * [链式编程](bian-cheng-fan-shi/bian-cheng-fan-shi/lian-shi-bian-cheng.md)
    * [响应式编程](bian-cheng-fan-shi/bian-cheng-fan-shi/xiang-ying-shi-bian-cheng/README.md)
      * [响应式编程的原理](bian-cheng-fan-shi/bian-cheng-fan-shi/xiang-ying-shi-bian-cheng/xiang-ying-shi-bian-cheng-de-yuan-li.md)
    * [函数式编程](bian-cheng-fan-shi/bian-cheng-fan-shi/han-shu-shi-bian-cheng.md)
    * [函数式、响应式、链式编程的结合](bian-cheng-fan-shi/bian-cheng-fan-shi/han-shu-shi-xiang-ying-shi-lian-shi-bian-cheng-de-jie-he.md)
  * [编程风格](bian-cheng-fan-shi/bian-cheng-feng-ge.md)
  * [比较](bian-cheng-fan-shi/bi-jiao.md)
* [流 Stream](liu-stream/README.md)
  * [抽象分类](liu-stream/chou-xiang-fen-lei.md)
  * [特性](liu-stream/te-xing.md)
* [软件架构模式](ruan-jian-jia-gou-mo-shi/README.md)
  * [耦合度](ruan-jian-jia-gou-mo-shi/ou-he-du/README.md)
    * [概念](ruan-jian-jia-gou-mo-shi/ou-he-du/gai-nian.md)
  * [衡量一个编程架构模式的好坏](ruan-jian-jia-gou-mo-shi/heng-liang-yi-ge-bian-cheng-jia-gou-mo-shi-de-hao-huai.md)
  * [软件架构模式的演化](ruan-jian-jia-gou-mo-shi/ruan-jian-jia-gou-mo-shi-de-yan-hua.md)
  * [分层架构](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/README.md)
    * [演化](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/yan-hua.md)
    * [MCV、MVP、MVVM演化](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mcvmvpmvvm-yan-hua.md)
    * [MV-X](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/README.md)
      * [数据流方向](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/shu-ju-liu-fang-xiang.md)
      * [构架界面架构](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/gou-jia-jie-mian-jia-gou.md)
      * [MVC](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvc/README.md)
        * [耦合度](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvc/ou-he-du.md)
        * [数据流](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvc/shu-ju-liu/README.md)
          * [数据流方向](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvc/shu-ju-liu/shu-ju-liu-fang-xiang.md)
        * [iOS的简单示例](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvc/ios-de-jian-dan-shi-li.md)
        * [优缺点](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvc/you-que-dian.md)
      * [MVP](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvp/README.md)
        * [耦合度](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvp/ou-he-du/README.md)
          * [和MVC比较](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvp/ou-he-du/he-mvc-bi-jiao.md)
        * [数据流](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvp/shu-ju-liu/README.md)
          * [数据流方向](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvp/shu-ju-liu/shu-ju-liu-fang-xiang.md)
        * [iOS简单例子](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvp/ios-jian-dan-li-zi.md)
        * [优缺点](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvp/you-que-dian.md)
      * [MVVM](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/README.md)
        * [耦合度](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/ou-he-du.md)
        * [数据流](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/shu-ju-liu/README.md)
          * [数据流向](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/shu-ju-liu/shu-ju-liu-xiang.md)
        * [iOS简单例子](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/ios-jian-dan-li-zi.md)
        * [优缺点](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/you-que-dian.md)
        * [疑惑点](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/yi-huo-dian/README.md)
          * [MVVM的数据绑定以及绑定的方式](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/yi-huo-dian/mvvm-de-shu-ju-bang-ding-yi-ji-bang-ding-de-fang-shi.md)
          * [响应式编程和 MVVM 关系](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvvm/yi-huo-dian/xiang-ying-shi-bian-cheng-he-mvvm-guan-xi.md)
      * [MVI](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/README.md)
        * [耦合度](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/ou-he-du.md)
        * [数据流](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/shu-ju-liu/README.md)
          * [数据传递的具体过程](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/shu-ju-liu/shu-ju-chuan-di-de-ju-ti-guo-cheng.md)
          * [数据流方向](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/shu-ju-liu/shu-ju-liu-fang-xiang.md)
        * [iOS例子](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/ios-li-zi.md)
        * [优缺点](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/you-que-dian.md)
        * [MVI架构的库](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/mvi/mvi-jia-gou-de-ku.md)
      * [比较](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/bi-jiao/README.md)
        * [MV-X的划分角度](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/bi-jiao/mvx-de-hua-fen-jiao-du.md)
        * [MVC、MVP、MVVM、MVI](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/bi-jiao/mvc-mvp-mvvm-mvi.md)
        * [MVVM vs MVI](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/bi-jiao/mvvm-vs-mvi/README.md)
          * [两者的单向数据流](ruan-jian-jia-gou-mo-shi/fen-ceng-jia-gou/mv-x/bi-jiao/mvvm-vs-mvi/liang-zhe-de-dan-xiang-shu-ju-liu.md)
* [设计模式](she-ji-mo-shi/README.md)
  * [疑问](she-ji-mo-shi/yi-wen/README.md)
    * [观察者模式和订阅者模式是不是同一个东西？](she-ji-mo-shi/yi-wen/guan-cha-zhe-mo-shi-he-ding-yue-zhe-mo-shi-shi-bu-shi-tong-yi-ge-dong-xi.md)

## 暂时

* [ReactiveSwift和RxSwift](zan-shi/reactiveswift-he-rxswift.md)
* [判断条件实现的效率](zan-shi/pan-duan-tiao-jian-shi-xian-de-xiao-l/README.md)
  * [固定且连续的条件值，switch比字典更高效](zan-shi/pan-duan-tiao-jian-shi-xian-de-xiao-l/gu-ding-qie-lian-xu-de-tiao-jian-zhi-switch-bi-zi-dian-geng-gao-xiao.md)
  * [跳转表](zan-shi/pan-duan-tiao-jian-shi-xian-de-xiao-l/tiao-zhuan-biao.md)
  * [编译器优化switch](zan-shi/pan-duan-tiao-jian-shi-xian-de-xiao-l/bian-yi-qi-you-hua-switch.md)
  * [编译器对if..else的优化](zan-shi/pan-duan-tiao-jian-shi-xian-de-xiao-l/bian-yi-qi-dui-if..else-de-you-hua.md)
