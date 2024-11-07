# MVC

MVC（Model-View-Controller）主要是做到了<mark style="color:red;">**关注点分离**</mark>

#### 1. 组件概述

* **Model（模型）**：
  * 代表应用程序的<mark style="color:orange;">数据和业务逻辑</mark>。
  * 负责数<mark style="color:orange;">据的获取、存储和管理，通常与数据库或外部API</mark>进行交互。
  * <mark style="color:orange;">不直接与用户界面交互</mark>，所有的状态和业务逻辑都集中在这里。
* **View（视图）**：
  * 负责<mark style="color:orange;">显示数据</mark>并向用户呈现界面。
  * <mark style="color:orange;">接收用户输入并将其传递给Controlle</mark>r进行处理。
  * 应用程序的表现层，通常使用<mark style="color:orange;">模板引擎或UI框架</mark>构建。
* **Controller（控制器）**：
  * <mark style="color:orange;">作为Model和View之间的中介</mark>，<mark style="color:orange;">处理用户输入并更新Model和View</mark>。
  * 接收来自View的输入，调用Model更新数据，然后更新View以反映这些变化。
  * <mark style="color:orange;">负责业务逻辑</mark>，<mark style="color:orange;">决定数据如何被展示和处理</mark>。

#### 2. 数据流

MVC模式通常遵循以下数据流：

1. 用户与View交互（例如，点击按钮、输入数据）。
2. View将用户输入传递给Controller。
3. Controller处理用户输入，可能会调用Model来获取或更新数据。
4. Model更新其状态并通知Controller。
5. Controller根据Model的变化更新View。
6. View重新渲染以显示更新后的数据。

#### 3. 特点

* **关注点分离**：MVC通过将应用程序的业务逻辑、数据和用户界面分离，提高了代码的可读性和可维护性。
* **灵活性**：不同的View可以使用相同的Model，允许开发者在不影响业务逻辑的情况下更改用户界面。
* **可测试性**：由于Controller与View分离，业务逻辑可以更容易地进行单元测试。

#### 4. 适用场景

* **Web应用程序**：MVC是许多Web框架（如Ruby on Rails、ASP.NET MVC、Django）使用的架构模式。
* **桌面应用程序**：MVC也常用于桌面应用程序，特别是在需要清晰分离界面和业务逻辑的情况下。

#### 5. 根据**Model**来划分 ——`主动模式`和`被动模式`

* **`被动模式`**：<mark style="color:orange;">不会主动将它的变化通知给View进行更新</mark>，而是由Controller更新View关于Model的变化； 而且只有Controller可以对Model进行更新；
* **`主动模式`**：<mark style="color:orange;">Model的修改会通知View更新，利用观察者模式</mark>：View为观察者，Model为被观察者。 在Web端，传统意义上的MVC是主动模式； 而在移动端，对数据变化频繁的场景，可以应用MVC的主动模式。

<figure><img src="../../../../.gitbook/assets/image (3).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>





####
