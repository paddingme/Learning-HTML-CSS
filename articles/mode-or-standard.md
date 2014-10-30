# 模式？标准！



<figure><img src="http://paddingme.qiniudn.com/taskbar.jpg" alt="电脑桌面任务栏"><figcaption>高(菜)端(鸟)front-end程序员的电脑桌面任务栏</figcaption></figure>


最近在工作中经常遇到浏览器兼容性的问题，让我焦头烂额，这里总结下浏览器的严格模式和怪异模式以及IE浏览下的文档模式和浏览器模式等内容。


### 严格模式和怪异模式

现代浏览器一般具有多种渲染模式：

 在“标准模式”(standards mode) 页面按照 HTML 与 CSS 的定义渲染，而在“怪异模式(quirks mode) 模式”中则尝试模拟更旧的浏览器的行为。 一些浏览器（例如，那些基于 Mozilla 的 Gecko 渲染引擎的，或者 Internet Explorer 8 在 strict mode 下）也使用一种尝试于这两者之间妥协的“近乎标准”(almost standards) 模式，实施了一种表单元格尺寸的怪异行为，除此之外符合标准定义。

通常，浏览器基于页面中文件类型描述的存在以决定采用哪种渲染模式；如果存在一个完整的 DOCTYPE 则浏览器将会采用标准模式，而如果它缺失则浏览器将会采用怪异模式。
例如，一个以如下 DOCTYPE 开始的网页将会触发标准模式：

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd">
```
如下 DOCTYPE 语法上是无效的，因为它包含公共标识符关键字 PUBLIC 却没有公共标识符（指示所用 HTML 版本的名称），也没有 HTML 文档类型定义的系统标识符 URL。这将会触发怪异模式：

```
<!DOCTYPE html PUBLIC>
```
此外，一个不含任何 DOCTYPE 的网页将会以 quirks 模式渲染。
对此一个值得一提的例外是微软的 Internet Explorer 6 浏览器，如果 DOCTYPE 之前有一个 XML 声明，不管是否指定完整的 DOCTYPE，它就会以 quirks 模式渲染一个页面。因此以如下代码开始的 XHTML 页面会被 IE 6 渲染为 quirks 模式：

```
<?xml version="1.0" encoding="utf-8"?><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN""http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```
在一定程度上，上述代码是有用的，然而它仅仅会对 IE 6 触发怪异模式。如果 DOCTYPE 之前有任何语句，quirks 模式在任何版本的 IE 中（截至 IE 9）同样会被触发。
例如，如果一个超文本文件在 DOCTYPE 前包含一个注释或者任何标签，IE (截至 9) 会使用 quirks 模式：

### IE的文档模式和浏览器模式

IE从IE8引入了文档兼容性开始有了浏览器模式和文档模式(按F12可见)

>“浏览器模式”:用于切换IE针对该网页的默认文档模式、对不同版本浏览器的条件备注解析、发送给网站服务器的用户代理（User-Agent）字符串的值。网站可以根据浏览器返回的不同用户代理字符串判断浏览器的版本和安装的功能，这样就可以向不同的浏览器返回不同的页面内容。

<figure><img src="http://paddingme.qiniudn.com/ie9-2ge-moshi.png" alt="IE8的浏览器模式"><figcaption>IE8的浏览器模式</figcaption></figure>

>“文档模式”用于指定IE的页面排版引擎（Trident）以哪个版本的方式来解析并渲染网页代码。切换文档模式会导致网页被刷新，但不会更改用户代理字符串中的版本号，也不会从服务器重新下载网页。切换浏览器模式的同时，浏览器也会自动切换到相应的文档模式。

<figure><img src="http://paddingme.qiniudn.com/ie9-2ge-moshi.png" alt="IE下的文档模式"><figcaption>IE9下的文档模式</figcaption></figure>

我的理解就是浏览器模式是指IE浏览器 向服务器发送请求时，告诉服务器自己是哪个浏览器哪个版本，这里是指告诉服务器我是IE7还是IE8或者9,然后浏览器根据收到的用户代理字段返回IE7或者IE8或者IE9的页面内容。

而文档模式则是指浏览器将服务器端发送过来的内容按照某种特定的浏览器（IE7，IE8，IE9等）来渲染页面。

这里还涉及到怪异模式（Quirks Mode），IE旧的怪异模式现在被称为IE5怪异模式,一般不予考虑。


###  DOCTYPE
为什么要研究这些呢，是为了强调按照标准写html语言的重要性，近来在工作中遇到的各种诡异的IEbug，花费了巨大精力调试，最后都是因为没有按照标准来写，没有doctyle头，标签没有闭合，导致各浏览器渲染不同诡异。

DOCTYPE是document type(文档类型)的简写，用来说明你用的XHTML或者HTML是什么版本。
其中的DTD(document type definition)叫文档类型定义，里面包含了文档的规则，浏览器就根据你定义的DTD来解释你页面的标识，并展现出来。
要建立符合标准的网页，DOCTYPE声明是必不可少的关键组成部分；除非你的XHTML确定了一个正确的DOCTYPE，否则你的标识和CSS都不会生效。

HTML5 (向后兼容，推荐使用):

```
<!DOCTYPE html>
```

HTML 4.01 Strict

This DTD contains all HTML elements and attributes, but does NOT INCLUDE presentational or deprecated elements (like font). Framesets are not allowed.

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```
HTML 4.01 Transitional

This DTD contains all HTML elements and attributes, INCLUDING presentational and deprecated elements (like font). Framesets are not allowed.

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```
HTML 4.01 Frameset

This DTD is equal to HTML 4.01 Transitional, but allows the use of frameset content.

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```

XHTML 1.0 Strict

This DTD contains all HTML elements and attributes, but does NOT INCLUDE presentational or deprecated elements (like font). Framesets are not allowed. The markup must also be written as well-formed XML.

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

XHTML 1.0 Transitional

This DTD contains all HTML elements and attributes, INCLUDING presentational and deprecated elements (like font). Framesets are not allowed. The markup must also be written as well-formed XML.

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

XHTML 1.0 Frameset

This DTD is equal to XHTML 1.0 Transitional, but allows the use of frameset content.

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

XHTML 1.1

This DTD is equal to XHTML 1.0 Strict, but allows you to add modules (for example to provide ruby support for East-Asian languages).

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
```

### IE兼容模式
IE 支持通过特定的 <meta> 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模式。

<meta http-equiv="X-UA-Compatible" content="IE=Edge">

### 内核控制Meta标签：让360浏览器默认使用极速模式打开网页

进来调试一个网页在IE、Chrome、Firefox下均表现正常，但是在360浏览器兼容模式下表现诡异。（国产的各种shell，我就呵呵了。）查查了内核控制Meta标签：让360浏览器默认使用极速模式打开网页，方法如下：

1. 网页头部加入

```
<meta name="renderer" content="webkit">
```
360浏览器就会在读取到这个标签后，立即切换对应的极速核。

2. 另外为了保险起见再加入

```
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
```
这样写可以达到的效果是如果安装了Google chrome frame，则使用GCF来渲染页面，如果没有安装GCF，则使用最高版本的IE内核进行渲染。


### 总结

作为前端，浏览器各种状况频发，诡异之处无所不在。最重要的是按照标准来规范自己的代码，另一方面了解各浏览器的特性，好规避bug,再者，不断debug，从坑里爬起来。




### 参考文章
1. [编码规范 by @mdo（墙裂推荐）](http://codeguide.bootcss.com/)
2. [关于浏览器模式和文本模式的困惑](https://www.imququ.com/post/browser-mode-and-document-mode-in-ie.html)
3. [IE 的浏览器模式和文本模式（二）](https://www.imququ.com/post/browser-mode-and-document-mode-in-ie-2.html)
4. [定义文档兼容性](http://msdn.microsoft.com/zh-cn/library/cc288325\(v=vs.85\).aspx)
5. [怪异模式](http://zh.wikipedia.org/wiki/%E6%80%AA%E5%BC%82%E6%A8%A1%E5%BC%8F)
6. [IE “浏览器模式”和“文档模式”的区别（IEfans）](http://www.iefans.net/shanchu-ie9-wenjianjia/)
7. [浏览器内核控制Meta标签说明文档浏览器内核控制Meta标签说明文档](http://se.360.cn/v6/help/meta.html)
