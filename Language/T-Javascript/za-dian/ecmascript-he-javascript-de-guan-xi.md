# ECMAScript 和 JavaScript 的关系



## ECMAScript 和 JavaScript 有着紧密的关系

**一、定义和起源**

1. ECMAScript：
   * <mark style="color:red;">**ECMAScript 是一种标准化的脚本语言规范**</mark>，由 Ecma International（欧洲计算机制造商协会）制定和维护。
   * 它**规定了脚本语言的语法、类型、语句、关键字、操作符等核心要素**，为不同的实现提供了一个统一的标准。
2. JavaScript：
   * JavaScript 是一种具体的编程语言，由 Netscape 公司的 Brendan Eich 在 1995 年创建。
   * 最初主要用于在网页上实现交互效果和动态内容。

**二、关系**

1. JavaScript 是 ECMAScript 的一种实现：
   * JavaScript 的语法和特性在很大程度上遵循 ECMAScript 规范。
   * 随着时间的推移，JavaScript 的不同版本不断发展，以适应新的需求和技术趋势，同时也努力保持与 ECMAScript 规范的兼容性。
2. ECMAScript 规范推动 JavaScript 的发展：
   * ECMAScript 规范的更新会引入新的语言特性和功能，JavaScript 实现（如不同的浏览器引擎和 Node.js）会逐步采用这些新特性。
   * 例如，**ECMAScript 6（ES6）引入了箭头函数、模板字符串、let 和 const 关键字等新特性**，JavaScript 引擎纷纷跟进实现这些特性，从而推动了 JavaScript 语言的发展。
3. 存在一些扩展和差异：
   * 虽然 JavaScript 努力遵循 ECMAScript 规范，但不同的 JavaScript 实现可能会在规范的基础上进行一些扩展。
   * 例如，浏览器中的 JavaScript 可能会提供与浏览器环境相关的特定 API（如 DOM 操作、BOM 等），这些并不是 ECMAScript 规范的一部分。
   * 此外，不同的 JavaScript 实现可能在性能、错误处理等方面存在一些差异。

**三、重要性**

1. 促进语言的统一和互操作性：
   * ECMAScript 规范确保了不同的 JavaScript 实现在核心语言特性上具有一定的一致性，使得开发者可以编写在不同环境中都能运行的代码。
   * 这有助于提高代码的可移植性和可维护性。
2. 推动语言的创新和发展：
   * ECMAScript 规范的不断更新为 JavaScript 带来了新的功能和改进，激发了开发者的创造力，促进了 JavaScript 在各个领域的应用和发展。

总之，ECMAScript 是 JavaScript 的规范标准，JavaScript 是 ECMAScript 的一种具体实现。它们相互影响、相互促进，共同推动了脚本语言的发展和应用。



***

## 遵循**ECMAScript 的编程语言**



遵循 **ECMAScript** 标准的语言主要是那些以 **JavaScript** 为基础，或者是与 JavaScript 紧密相关的语言和环境。ECMAScript 是一种规范，定义了 JavaScript 的核心语法、特性和行为。以下是一些遵循或基于 ECMAScript 的编程语言和环境：

#### 1. **JavaScript**

* **JavaScript** 是 ECMAScript 规范的最直接实现。自 **ECMAScript 1** 以来，JavaScript 一直紧密遵循 ECMAScript 规范，随着 ECMAScript 的更新（如 ES6/ES2015、ES7/ES2016 等），JavaScript 也在不断演进。

#### 2. **TypeScript**

* **TypeScript** 是 JavaScript 的静态类型超集，添加了类型系统和其他高级语言功能。TypeScript 代码最终编译为遵循 ECMAScript 标准的 JavaScript，因此它与 ECMAScript 完全兼容。

#### 3. **JScript**

* **JScript** 是微软对 ECMAScript 的实现，早期版本主要用于 **Internet Explorer** 浏览器的脚本处理。JScript 基于 ECMAScript 标准，但由于浏览器厂商的差异，JScript 有一些 Microsoft 专有的特性。

#### 4. **ActionScript**

* **ActionScript** 是由 Adobe 设计的一种脚本语言，最初用于 **Flash** 平台开发动画和交互应用。ActionScript 3.0 基于 ECMAScript 4 规范，并加入了静态类型等特性。虽然 Flash 已逐渐淘汰，但 ActionScript 是 ECMAScript 的一个早期扩展。

#### 5. **CoffeeScript**

* **CoffeeScript** 是一种编程语言，它将代码编译为 ECMAScript 兼容的 JavaScript。虽然它在语法上与 ECMAScript 有较大区别，但其目标是生成符合 ECMAScript 规范的 JavaScript 代码。

#### 6. **Dart（早期版本）**

* **Dart** 是 Google 开发的编程语言，最初它是为了替代 JavaScript 而设计的，Dart 1.x 曾支持编译为 ECMAScript 兼容的 JavaScript 代码。然而，现代 Dart 主要作为 Flutter 框架的核心语言，已经独立于 ECMAScript 规范，但仍支持编译成 JavaScript 运行在浏览器上。

#### 7. **Elm**

* **Elm** 是一种函数式编程语言，主要用于构建 web 应用。虽然 Elm 有自己独特的语法和特性，但它最终会编译为遵循 ECMAScript 规范的 JavaScript，便于在浏览器中运行。

#### 8. **Google Apps Script**

* **Google Apps Script** 是 Google 提供的基于 ECMAScript 规范的脚本语言，允许开发者编写自动化脚本来与 Google 产品（如 Gmail、Google Sheets 等）进行集成。它的语法与 ECMAScript 保持高度一致。

#### 9. **Nashorn (JavaScript Engine for Java)**

* **Nashorn** 是 Java 平台上的一个 JavaScript 引擎，它基于 ECMAScript 规范，允许 JavaScript 代码在 Java 虚拟机 (JVM) 上运行。Nashorn 主要用于 Java 应用程序中嵌入和执行 JavaScript 代码。

#### 10. **VBScript (类似于 ECMAScript，非完全遵循)**

* 虽然 **VBScript** 不是完全基于 ECMAScript，但它是微软开发的一种类似于 JavaScript 的脚本语言。它与 ECMAScript 有一定的相似性，特别是在浏览器端早期用作网页脚本的替代品，但它并不完全遵循 ECMAScript 标准。

#### 总结

以下语言严格或部分遵循了 ECMAScript 标准：

* JavaScript
* TypeScript
* JScript
* ActionScript
* CoffeeScript
* Google Apps Script
* Nashorn (JavaScript on JVM)

此外，像 **Elm**、**Dart（早期版本）** 这些编译为 JavaScript 的语言虽然不直接遵循 ECMAScript 规范，但其编译后的输出符合 ECMAScript 标准，使得它们能够在 JavaScript 环境（如浏览器）中运行。

ECMAScript 作为 JavaScript 背后的标准，直接影响了众多语言的发展，尤其是在 Web 和客户端开发方面的语言。
