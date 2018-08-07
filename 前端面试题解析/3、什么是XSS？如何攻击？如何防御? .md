
#### xss 跨站脚本攻击，（cross site scripting）,
> 为了区分css所以起名为xss,xss攻击分为两类

1、url参数注入
2、存储到DB后读取注入。

> xss一般通过以下方法注入攻击

1、HTML节点内容
2、HTML属性
3、Javascript代码
4、富文本

#### 防御

1、一般浏览器都自带防御xss，但在脚本中xss不能被拦截。
可以通过设置X-XSS-Protection: 1 
php设置 header("X-XSS-Protection: 1; mode=block"); 
当检测到xss攻击时阻止加载页面。

2、一般最常用的防御手段是转义接收的数据，不被浏览器识别。
可以通过内置函数转义 、DOM解析白名单、 第三方库实现
比如php中常用的方法 strip_tags() htmlspecialchars()
php内置类 DOMDocument class 实现DOM白名单
第三方库 HTML Purifier

3、最有效的方法
CSP （Content Security Policy） 内容安全策略。
用于指定哪些内容可执行。
用http的头规定了哪些内容可被执行。
php用法
header("Content-Security-Policy: script-src 'self'");
了解更多：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP