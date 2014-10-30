# 学习CSS布局


这是偶尔看到的一篇学习CSS布局的文章，对于我这个菜鸟来说真是受益匪浅，对CSS布局一下子拨云见雾的感觉。你可以到[这里](http://zh.learnlayout.com/)仔细研究阅读，相信你会和我一样兴奋和豁然开朗。而下面是我在此基础上总结的内容，以便后来查阅使用。


+ **"display"属性**

  每个元素都有默认的display属性，一般是block或者inline,block表示块级元素，而inline表示行内元素。block元素（如`div`、`table`、`p`、`form`等）会新开始一行并尽可能撑满容器。而inline元素（如`span`、`a`等）即行内元素不会打破包裹它的容器的布局。另一个常用的display值为`none`，`display:none`通常是被JavaScript用来在不删除元素的情况下隐藏或显示该元素。
  其他的display值还有list-item和table等，详情可以参见[这里](https://developer.mozilla.org/en-US/docs/Web/CSS/display),你可以随时随地人工改变一个元素的display值。常见的是：把`li`改为`display:inline`制作水平菜单。

+ **marigin:auto**

  如何使一个元素居中，并且不用担心小屏幕会显示出滚动条：(max-width 支持IE7+)
<code><pre>
    #main{
    max-width:600px;
    margin:0 auto;
}</pre></code>

+ **盒模型**

 盒模型的宽度高度我们知道要通过计算（真正的宽度=width+2*padding+2*border）我们使用`box-sizing`来改进它，当设置一个元素为`box-sizing:border-box`时，此元素的内边距和边框不会增加该元素的宽度。支持IE8+，如果要在所有浏览器中使用该属性，则可以利用下面的代码：
<code><pre>
    *{
    -webkit-box-sizing:border-box;
    -moz-box-sizing:border-box;
        box-sizing:border-box;
}
</pre></code>

+ **position**

  `position`主要由static、absolute、relative、fixed等值。 
  
   >1. static 是默认值，表示没有被定位。
   >2. relative 相对定位，相对于它在正常文档流中，通过top、right、bottom、left作用值产生偏移。而其他元素不会调整位置来弥补它偏离后剩下的间隙。
   >3. fixed 固定定位，相对于浏览器窗口，意味着即使页面滚动，它还是会停留在相同的位置。（移动浏览器对fixed支持很差，解决方案参考[这里]（http://bradfrostweb.com/blog/mobile/fixed-position/）。
   >4. absolute 是相对于最近的被定位的祖先元素产生的偏移，如果没有，它是相对文档的body元素，并且它会随着页面滚动而移动。


+ **float**

 如前篇所述，最开始产生float的作用就是使文字环绕图片，其本质就是包裹和破坏，它脱离了正常的文档流，可能会导致溢出，所以要clearfix hack（清除浮动），清除浮动的方法有很多种，可以参考[上篇文章](http://padding.me/blog/2014/04/19/float-label-in-css/)张鑫旭写的，[这里](http://stackoverflow.com/questions/211383/which-method-of-clearfix-is-best)有更多的讨论


+ **媒体查询**

 针对响应式设计，，让网站针对不同浏览器和设备相应。

 <code><pre>
 @media screen and (min-width:600px) {
  nav {
    float: left;
    width: 25%;
  }
  section {
    margin-left: 25%;
  }
}
@media screen and (max-width:599px) {
  nav li {
    display: inline;
  }
}
</pre></code>

在[MDN文档](https://developer.mozilla.org/en-US/docs/CSS/Media_queries)中有更多关于媒体查询的知识。使用 [meta viewport](http://dev.opera.com/articles/view/an-introduction-to-meta-viewport-and-viewport/) 之后可以让你的布局在移动浏览器上显示的更好。

+ **inline-block**

  使用行内联。IE6和IE7支持看[这里](http://blog.mozilla.org/webdev/2009/02/20/cross-browser-inline-block/)
  使用inline-box要注意以下：
     * vertical-align 属性会影响到 inline-block 元素，你可能会把它的值设置为 top 
     * 需要设置每一列的宽度
     * 如果HTML源代码中元素之间有空格，那么列与列之间会产生空隙

+ **column**
<code><pre>
 .three-column {
  padding: 1em;
  -moz-column-count: 3;
  -moz-column-gap: 1em;
  -webkit-column-count: 3;
  -webkit-column-gap: 1em;
  column-count: 3;
  column-gap: 1em;
}
</pre></code>
CSS columns是很新的标准，所以你需要使用前缀，并且它不被IE9及以下和Opera Mini支持。还有许多和 cloumn 相关的属性，点击[这里](http://quirksmode.org/css/columns/)了解更多

+ **flexbox**

新的 flexbox 布局模式被用来重新定义CSS中的布局方式。很遗憾的是最近规范变动过多，导致各个浏览器对它的实现也有所不同。具体例子可以参考[这里](http://zh.learnlayout.com/flexbox.html)


+ **其他框架**

 例如bootstrap的12格流式布局等等。