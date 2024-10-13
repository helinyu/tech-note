# MVP

基于MVC的改良

#### 1. 组件概述

* **Model（模型）**：
  * 负责应用程序的数据和业务逻辑。
  * 管理数据的获取、存储和处理，通常与数据库或外部API进行交互。
  * 由Presenter调用来获取或更新数据。
* **View（视图）**：
  * 负责显示用户界面和呈现数据。
  * 处理用户输入，并将其传递给Presenter进行处理。
  * 仅包含UI元素和展示逻辑，不包含任何业务逻辑。
* **Presenter（呈现器）**：
  * 作为Model和View之间的中介，负责处理用户输入、更新Model和控制View的显示。
  * 接收来自View的输入，调用Model获取或更新数据，然后更新View以反映这些变化。
  * 执行所有的业务逻辑，通常不直接与UI元素交互。

#### 2. 数据流

MVP模式的典型数据流如下：

1. 用户与View交互（例如，点击按钮、输入数据）。
2. View将用户输入传递给Presenter。
3. Presenter处理用户输入，可能会调用Model来获取或更新数据。
4. Model更新其状态并通知Presenter。
5. Presenter根据Model的变化更新View。
6. View重新渲染以显示更新后的数据。

#### 3. 特点

* **关注点分离**：MVP通过将应用程序的业务逻辑、数据和用户界面分离，提高了代码的可读性和可维护性。
* **可测试性**：Presenter可以独立于View进行单元测试，因为它不依赖于具体的UI实现。
* **灵活性**：View可以很容易地更换，Presenter可以在不同的View之间复用，允许开发者在不影响业务逻辑的情况下更改用户界面。

#### 4. 适用场景

* **桌面应用程序**：MVP常用于需要频繁更新UI的桌面应用程序，如Java Swing、Windows Forms等。
* **移动应用程序**：MVP也广泛应用于Android应用程序开发，因为它可以帮助组织代码并提高可测试性。

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<mark style="color:orange;">View它持有Presenter作为变量（和MVC的差别）</mark>。

> View持有Presenter，所以Presenter中的View应该声明为weak或unowned，避免循环。



**优点**：解耦View和Controller之间的耦合，将View和Presenter区分得更加清楚。将业务划分更加精细\
**缺点**：View所有的交互都传给Presenter处理，一旦项目功能增加了，View的代码和Presenter的代码将会增加。 相比MVC在C一个文件里面就解决，MVP总代码量会增加。App维护成本和文件会增大。\


