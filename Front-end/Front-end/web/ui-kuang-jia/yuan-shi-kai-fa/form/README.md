# Form

### 1.1 什么是表单？

在网页中主要负责<mark style="color:red;">**数据采集功能**</mark>，HTML中\<form>标签就是用来采集数据的，并且通过form的操作，把采集到的数据提交到服务器进行处理。

<figure><img src="../../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

### 1.2 表单的组成部分

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 1.3 \<form>标签属性

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 1.4 表单的同时提交以及缺点

#### 1、什么是表单的同步提交

通过点击submit按钮，触发表单提交的操作，从而使页面跳转到action URL的行为，叫做表单的同步提交。

#### 2、表单同步提交的缺点

① form表单提交后，整个页面会发生跳转，跳转到action URL所指向的地址，用户体验很差

② form表单表单提交后，之前的页面状态和数据会丢失

#### 3、如何解决表单同步提交的缺点

如何使用表单提交数据，则会导致一下两个问题：

①：页面会发生跳转

②： 页面之前的的状态和数据会丢失 —— 其实就是页面跳转了之后丢失了这些

**解决方案**：表单只负责采集数据，Ajax负责将数据提交到服务器。



