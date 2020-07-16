# 跨域问题

## 概述
跨域是由浏览器的同源策略（一种禁止使用js访问其他domain资源，包括 cookie，api，iframe 等等）所产生的一系列试图打破同源策略限制的方法。

早期的同源策略非常死板，比如 ajax 不能访问其他 domain 的 api，但是实际应用中 api 往往会部署在不同于站点的 domain 下，即，这是个刚需。早期，解决这个问题的办法是使用 script 标签产生的 http get
请求不会被同源策略限制这个“漏洞”，来访问后台 api，这就是 jsonp。之后，CORS 开始普及，api 的开发者通过几个 http header “定义” 可以合法访问 api 的 domain。

同样，对于共享 cookie，逐渐从早期的各种奇技淫巧过度为现在依靠子域名的管理来合法共享。而不同 document 之间（frame，window，tab）之间浏览器不同 frame、tab，window 之间的数据通信则逐渐被
window.postMessage 所取代，早期常见的办法是监测窗口的可读写属性（比如hash）来间接沟通信息。

## 误解
同源策略是约束 js 的手脚，所以任何试图通过 js 来绕过同源的办法都是白日梦。jsonp 利用了 script 标签，后台填充 callback 数据，不算是纯 js。CORS 则是完全与 js 无关。

同源策略不是一种“缺陷”，有缺陷的是早期的同源策略没有考虑到之后 web 发展的迅猛，多 domain 并存形成复杂的 app 矩阵成为常态，比如阿里巴巴旗下的很多 app，后台，就部署在多个不同的 domain 下。同源
策略是不利于这种复杂生态的。好在 CORS 和 window.postMessage （主要是前者）的发布基本上修复了这个“缺陷”。

跨域是一类技术，目的是绕过同源策略。早期的做法多是利用同源策略的“漏洞”，间接达到目的。后来的技术是合法的绕过，或者更准确是通过，同源策略的防火墙。

## 与“跨域”共舞 - 2020 年
跨域不是什么高深的操作，但是小心别把问题弄得太复杂。比如：
1.明明有 CORS 可以用，非要 jsonp。
2.明明有 window.postMessage 可以用，非要用更老的技术。

好的技术应该更方便好用，钻研老技术，尤其是当年为了绕过有些限制发明的技术，完全是浪费时间。

## CORS 与 Nginx
CORS 的分两块，第一，api response 的 http header 中添加一些 header（哪些 domain 可以访问，以及访问方法，等细节），表示此 api 允许被哪些 domain 访问。第二，浏览器接收到 response 之后，阅读这些 header，判断当前 domain
（发出 ajax 的 domain）是否符合规则。如符合，则将 response 转交给对应的 domain（ajax的callback），如不符合，则抛出错误。

如果是单个后台服务，可在 api 代码里添加 CORS 支持。如果服务多，规则又复杂，Nginx 是更好的选择。

## 禁用同源策略
在开发 app 过程中，经常需要暂时的关闭同源策略，比如，当后台 api 没有对 local host 开放 CORS。可以通过简单地启动命令来禁用同源策略，下面是 chrome 的例子：

### Windows
1. 找到 chrome 快捷方式，或者手动创建一个
2. 打开属性，在“目标”里追加 ```--disable-web-security --disable-gpu --user-data-dir=%LOCALAPPDATA%\Google\chromeTemp```
### OSX
命令行输入
```
open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
```
### Linux
命令行输入
```
google-chrome --disable-web-security
```

> chrome 启动后会在工具栏下面显示警告信息，提示安全风险，忽略即可。

***注意：请不要再已经关闭同源策略的浏览器里登录重要网站，以免造成个人信息泄露，资产损失。***

参考：https://alfilatov.com/posts/run-chrome-without-cors/
