# SDWebImage

> Bugly上显示的bug&#x20;
>
> \#1316 SIGSEGV
>
> SEGV\_ACCERR
>
> libsystem\_platform.dylib \_\_platform\_memmove

<figure><img src="../../../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

上面是崩溃的崩溃信息和系统版本以及 调用栈

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

#### 修改方案： 因为上个版本修改在iOS 16.7 版本报错，没有注意看更低的版本， 所以，我们要兼容到iOS 17 之前的统一处理。&#x20;

<figure><img src="../../../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

这上面修改的知识针对iOS 16.7 版本的，而现在有15.8 的， 我们准备做针对17.0之前的处理。看了都是15.8 的7 plus ,应该都是升级不了的，做了处理。&#x20;

应该修改为17 之前的处理。&#x20;















