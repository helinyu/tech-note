# 3、HTTP请求问题（兼容）

在iOS9 中，系统将原http协议改成了默认https协议，使用 TLS1.2 SSL加密请求数据。可以通过升级支持HTTPS协议请求，也可以通过设置强制使用HTTP请求。在Info.plist中添加NSAppTransportSecurity类型Dictionary。在NSAppTransportSecurity下添加NSAllowsArbitraryLoads类型Boolean,值设为YES。部分第三方应用不支持HTTPS，需要在在info.list设置HTTP请求白名单，允许部分请求可以是HTTP。

```
<key>LSApplicationQueriesSchemes</key>  
	  <array>          	
<!-- 微信 URL Scheme 白名单-->     
    	 <string>wechat</string>   
      	 <string>weixin</string>   
       </array>

```
