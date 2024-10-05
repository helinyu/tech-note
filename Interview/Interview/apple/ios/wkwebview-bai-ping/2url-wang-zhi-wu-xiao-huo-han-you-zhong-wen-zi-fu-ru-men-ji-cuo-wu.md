# 2、URL网址无效或含有中文字符（入门级错误）

&#x20;APP内展示URL的来源主要是后端返回或前端拼接，甚至前端hardcode，网址存在不确定性，可能是无效或含有中文字符。大部分浏览器是能打开带有中文字符的网络地址，但是iOS的内嵌网页加加载框架无论是UIWebView还是WKWebView，都不能打开带有中文字符的网络地址，需要先对地址字符串做UTF8转码。

{% code overflow="wrap" %}
```
urlString = [urlString stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];
```
{% endcode %}

