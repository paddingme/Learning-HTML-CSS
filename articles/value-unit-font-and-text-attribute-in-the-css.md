# CSS中的值和单位、字体以及文本属性


这几天在学习[CSS权威指南](http://www.amazon.cn/CSS%E6%9D%83%E5%A8%81%E6%8C%87%E5%8D%97-%E8%BF%88%E8%80%B6/dp/B0011F5SIC/ref=sr_1_1?ie=UTF8&qid=1399054787&sr=8-1&keywords=css+%E6%9D%83%E5%A8%81%E6%8C%87%E5%8D%97),学习了CSS中的值和单位、字体以及文本属性，这里做一个相关总结，主要总结我认为重要的知识点。

##1. 值和单位##
CSS里的值和单位，主要分为绝对长度单位：`in`(英寸)、`cm`(厘米)`mm`(毫米)、`pt`(点，标准印刷度量单位)、`pc`(派卡，印刷术语),以及相对长度单位：`em`,`ex`,`px`。

我们主要使用`em`和`px`，`ex`指所用字体中小写x的高度,我们无情得忽视它。“相对”相对“绝对”的好处我们已然了解，例如url链接，我们不用关注外部url地址如何变化，相对路径没问题，我们便可以各种超链接。这里的相对长度单位也是同样的道理。`em`相对于给定字体的font-size值。现代浏览器字体默认大小为16个像素。如果一个元素的font-size为14px,那么对于该元素，1em=14px。这个值可能会随元素的不同而不同，另在设置字体的大小的时，em的值会相对于父元素的字体大小改变。总得来说，就是**em依赖于最近的字体大小**(不要惯性的以为依赖于原先body设定的或者浏览器默认的值。)

而`px`就是像素，对于显示器屏幕分辨率而言。当然`%`同`em`。（注意理解:`%`这个值可以是任意的：可能是同一个元素另一个属性的值，也可以是从父元素继承的一个值，或者是祖先元素的一个值。）


至于要用`px`还是`em`，老版本的IE浏览器不支持像素的缩放，所以用`px`取代`em`，另使用em可以省去很多冗余的工作，例如设置了body里的字体大小，后面的元素内的字体大小全部设置为em大小，这样改动的话只需要改动body里的字体大小，而不用每个元素改动px大小，再次提醒**em依赖于最近的字体大小**。将行距(line-height)，和纵向高度的单位都用em。保证缩放时候的整体性。px常使用在图片大小上。

[这篇文章](http://blog.alphatr.com/em-and-px-in-css.html)也有一定参考意义，可以一看。

##2. 颜色##
CSS中颜色取值主要由以下几种方法：

* CSS命名颜色。在CSS2.1中，CSS规范定义了17个颜色名。
* 用RGB指定颜色。可以使用0~255取值或者0%~100%。

```
h1 {color:rgb(100%,50%,50%);}
h2 {color:rgb(255,132,123);}
```
* 十六进制的RGB颜色。将三个介于00-FF的十六进制数连起来，就可以设置一种颜色。
```
h1 {
	color:#FF0000;
}
```
可以简写为
```
h1{
	color:#F00;
}
```
浏览器会取每一位，并将其复制成两位。
* RGBA颜色表示。在RGB的基础上加了一个Alpha通道.它规定了对象的不透明度。lpha 参数是介于 0.0（完全透明）与 1.0（完全不透明）的数字。浏览器支持：IE9+、Firefox 3+、Chrome、Safari 以及 Opera 10+。
```
p {
 background-color:rgba(255,0,0,0.5);
}
```
* HSL颜色和HSLA不做赘述。

##3. 字体##
CSS通常使用`font-family`定义使用什么字体，`font-size`定义字体大小，`font-style`定义斜体字，
`font-variant`定义小型的大写字体，`font-weight`定义字体的粗细，`font`统一定义字体的所有属性。


####font-family####
   font-family取值: `[[ <family-name> | <generic-family> ] [, <family-name>| <generic-family>]* ] | inherit`

 family-name:指一系列字体名称
 而generic-family是指一般性字体名称即以下五种通用字体系列。
CSS定义了五种通用字体系列（font-family）：

 + Serif字体——这些字体成比例，而且有上下短线,Sefit字体包括Times、Georigia和New Century Schoolbook等。
 + Sans-serif字体——字体成比例，但是没有上下短线。Sans-sefit字体包括Geneva,Verdana,Arial和Univers等。
 + Monospace字体——不成比例（模拟打印设备打出的文本），每个字符的**宽度**完全相同,上下短线可能有可能无。monospace字体包括Courier、Courier New、Andale Mono 等。
 + Cusrive字体——模仿人的手写体。包括Zapf Chancery、Anthou、Comic Sana等。
 + Fantasy字体——在上述四种字体之外的，不能用任何特征来定义的字体包括：Wesrern、Woodblock和Kinggong等。

说明：

* 想要显示的字体一定要是你计算机中有的,否则不会按照你期望的显示.上面的第三个示例说明如果有宋体就显示宋体否则显示Arial字体
* [字体名1 , 字体名2 , \*],其中的星号\*,表示可以继续增加字体名.如果用户计算机没有安装,你定义的字体名1,系统会自动使用字体名2,如果没有字体名2,系统就再查找字体名3,如果都没有,将使用系统的默认字体
* family-name代表系列性字体的名称,比如可以使用逗号分开,的方式取一系列的值("Times","Arial","Courier"等)
* generic-family代表一般性字体名称,每个名称都可以代表一系列的字体,比如"serif", "sans-serif", "cursive", "fantasy", "monospace"
* 用逗号来分隔每一个值,最好在最后有一个基本字体(generic-family)
* 使用中文字体或者英文名称超过一个单词的字体时要使用"(冒号)扩起来,比如"Times News Roman","宋体"
* 现代浏览器字体默认的设置为“宋体/simsun字体 16像素”

(留坑：[paddingme](http://padding.me)博客字体默认设置为small,而[http://www.zaibc.com/](http://www.zaibc.com/)的字体设置为
`body {
font: 13px Tahoma, Helvetica, Arial, "\5b8b\4f53", sans-serif;
}`) 很奇怪在我电脑上(windows7,chrome33.0.1750.146 )显示正常，而在同学的电脑上(mac，chrome版本未知）我博客的字体竟然比zaibc的字体小)理论上，small为13px，为什么不一样大呢？难道是浏览器渲染的问题？等我入手大MAC再做详细对比研究。当然HTML的big,small标签已经被w3c抛弃)

另关于默认字体可以查阅[女施主的博文中](http://saibeixuer.blog.163.com/blog/static/74770377201075111628356/)详细解析了淘宝的字体，可以围观，做深入了解。还有这位[男施主的博文](http://www.iyunlu.com/view/css-xhtml/default-web-font-style-1.html)和[这一篇博文](http://iyunlu.com/view/css-xhtml/default-web-font-style-2html.html),玉伯的文章找不到了很遗憾。张鑫旭的[这篇博客](http://www.zhangxinxu.com/wordpress/?p=874)也相当有趣，建议观看，提供一个新的视角关于字体设置。还强烈推荐[这篇博客](http://lepture.com/zh/2014/chinese-fonts-and-yue-css)，博主对中文字体确有研究，所以他的网站[阅乎](http://yuehu.io)阅读体验非常好。**字体真是一门大学问!**


##4. 文本属性##



<br>

参考文章：

+ [http://www.1z1b.com/one-blog-a-week/px-em-pt/#comment-17058](http://www.1z1b.com/one-blog-a-week/px-em-pt/#comment-17058)
+ [http://www.dreamdu.com/css/css_colors/](http://www.dreamdu.com/css/css_colors/)
+ [http://www.w3school.com.cn/cssref/css_colors_legal.asp](http://www.w3school.com.cn/cssref/css_colors_legal.asp)
