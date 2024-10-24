# Create-dmg

#### 1、作用 <a href="#id-1-zuo-yong" id="id-1-zuo-yong"></a>

主要用来将mac上的xx.app的应用打包成为dmg应用

#### 2、实践过程 <a href="#id-2-shi-jian-guo-cheng" id="id-2-shi-jian-guo-cheng"></a>

在[github](https://github.com/create-dmg/create-dmg)上是开源的；

官方提供了安装的命令： `brew install create-dmg`

如果上面的这个安装的软件，在执行的时候老是出现错误，可以换一种方式

`npm install -g create-dmg`

重新安装尝试

#### 3、执行创建过程 <a href="#id-3-zhi-xing-chuang-jian-guo-cheng" id="id-3-zhi-xing-chuang-jian-guo-cheng"></a>

**3.1 、archieve**

将xcode上的线面archive，获取到里面的dmg文件拷贝到一个路径下

操作：

![](https://hly-tech.gitbook.io/\~gitbook/image?url=https%3A%2F%2F448331874-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FIAjQgZnbQIolEePFfNLh%252Fuploads%252FlOixnjmbKGD9IQWLW1sx%252Fimage.png%3Falt%3Dmedia%26token%3D35113133-d8e6-4c2a-a596-29f22b6dc11a\&width=768\&dpr=4\&quality=100\&sign=2fc59934\&sv=1)

**3.2、将xx.app 创建为xx.dmg 项目**

`create-dmg VCB.app`

这样就通过VCB.app创建了一个VCB.dmg 的mac安装包了。

#### 4、提供给其他人使用 <a href="#id-4-ti-gong-ji-qi-ta-ren-shi-yong" id="id-4-ti-gong-ji-qi-ta-ren-shi-yong"></a>

**1、直接发给别人**

**2、听过github上的release**

vcb在release上

**3、通过brew， 让别人安装**

[创建brew的源软件](https://hly-tech.gitbook.io/tools/brew)
