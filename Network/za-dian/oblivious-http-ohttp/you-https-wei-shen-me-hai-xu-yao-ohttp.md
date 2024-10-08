# Page 1

HTTPS确实通过加密和身份验证提供了网络通信的安全性，但OHTTP（Oblivious HTTP）的出现是为了解决HTTPS在隐私保护方面的局限性，特别是在防止去匿名化攻击方面。以下是相关介绍：

#### HTTPS的加密原理

HTTPS通过在HTTP协议上加入SSL/TLS协议来加密数据传输，确保数据在传输过程中的机密性和完整性。

#### HTTPS的隐私保护局限性

尽管HTTPS提供了加密保护，但它仍然存在一些隐私保护方面的局限性：

* **IP地址暴露**：HTTPS无法隐藏用户的IP地址，网络运营商和应用程序提供商仍然可以通过IP地址追踪用户。
* **去匿名化攻击**：通过分析用户的行为模式，攻击者有可能揭示用户的真实身份。

#### OHTTP的隐私保护优势

OHTTP通过<mark style="color:red;">引入中继服务来进一步保护用户的隐私</mark>，其优势包括：

* **隐藏用户IP地址**：通过中继服务转发请求，隐藏用户的真实IP地址，防止网络运营商和应用程序提供商的追踪。
* **防止去匿名化攻击**：中继服务移除所有能识别用户身份的信息，增加攻击者去匿名化的难度。

#### OHTTP的应用场景

OHTTP适用于需要高级别隐私保护的应用程序和服务，如匿名浏览、医疗保健数据共享等，特别是在网络安全领域，可以帮助防止通过分析用户请求模式来去匿名化用户身份的攻击。

总之，虽然HTTPS提供了基本的安全性和数据完整性保护，但OHTTP通过其独特的隐私保护机制，特别是在防止去匿名化方面的优势，为网络通信提供了更高级别的安全保障。



## [Oblivious DNS：堵住互联网最大的隐私漏洞](https://cloud.tencent.com/developer/news/175975)

\


