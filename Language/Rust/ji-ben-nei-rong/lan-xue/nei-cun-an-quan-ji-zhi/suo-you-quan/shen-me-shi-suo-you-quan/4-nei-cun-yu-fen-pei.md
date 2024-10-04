# 4、内存与分配

<figure><img src="../../../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

\


<figure><img src="../../../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

假如你在其他语言中接触过浅度拷贝 （shallow copy）和深度拷贝 （deep copy）这两个术语，那么你也许会将这里复制指针、长度及容量字段的行为视作浅度拷贝。但由于Rust同时使第一个变量无效了，所以我们使用了新的术语移动 （move）来描述这一行为，而不再使用浅度拷贝。



<figure><img src="../../../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

这里还隐含了另外一个设计原则：Rust永远不会自动地创建数据的深度拷贝。因此在Rust中，任何自动的赋值操作都可以被视为高效的。

`变量和数据交互的方式：克隆`

当你确实 需要去深度拷贝String堆上的数据，而不仅仅是栈数据时，就可以使用一个名为clone的方法。

<figure><img src="../../../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

