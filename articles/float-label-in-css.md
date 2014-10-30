# CSS 中的float标签

CSS中允许浮动任何元素，浮动是指元素浮动在左边或者右边，而使其他的内容“围绕”这个元素。
> ##float
> 值：left|right|none|inherit

例如把一个图像浮动到左边，
`<img src="b4.gif" style="float:left;" alt="b4">`

对于浮动元素有几点要记住：
1. 会以某种方式将浮动元素从文档的正常流中删除，但是一个元素浮动，其他内容会”围绕“该元素。
2. **浮动元素的外边距不会合并！**

浮动元素的包含块是其最近的块级祖先元素。此外，**浮动元素会生成一个块级框，而不论这个元素本身是什么。**

有一系列规则控制着浮动元素的摆放：

1. 浮动元素的左（或右）外边界不能超出其包含块的左（或右）内边界。
2. 浮动元素的左（或右）外边界必须是源文档中之前出现的左浮动（或右浮动）元素的右（左）外边界，除非后出现浮动元素的顶端在先出现浮动元素的低端下面。（不必担心一个浮动元素与另一个浮动元素重叠）。
3. 左浮动元素的右外边界不会在其右边右浮动元素的左外边界的右边。（防止浮动元素相互重叠）。
4. 一个浮动元素的顶端不能比其父元素的内顶端更高。如果一个浮动元素在两个合并外边距之间，放置这个浮动元素时就好像在两个元素之间有一个块级父元素。
5. 浮动元素的顶端不能**比之前所有浮动元素或块级元素的顶端**更高。
6. 如果源文档中一个浮动元素之前出现另一个元素，浮动元素的顶端不能比包含该元素所生成框的任何行框的顶端更高。
7. 左（或右）浮动元素的左边（或右边）有另一个浮动元素，前者的右外边界不能在其包含的右（左）边界的右边（左边）。（如果没有足够的空间，浮动元素会被挤到一个新的”行“上）。
8. 浮动元素必须尽可能高地放置。
9. 左浮动元素必须向左尽可能远，右浮动元素必须向右尽可能远。位置越高，就会向右或向左浮动得越远。

如上这些浮动规则只处理了浮动元素和其父元素的左、右和上边界，而未涉及下边界。CSS2.1规定，浮动元素会延伸，从而包含其所有后代浮动元素。故通过将父元素设置为浮动元素，就可以把浮动元素包含在其父元素内。


负外边距可能导致浮动元素移到其父元素的外面。还有一种方法，让浮动元素比其父元素更宽。

若一个浮动元素与正常流中的内容发生重叠：

1. 行内框与一个浮动元素重叠时，其边框、背景和内容都在该浮动元素”之上“显示。
2. 块框与一个浮动元素重叠时，其边框和背景在该浮动元素”之下“显示，而内容在浮动元素”之上“显示。

##清除浮动##
> ##clear
> 值：left|right|both|none|inherit
> 应用于块级元素


在google查询float标签相关文章发现下面两篇文章特别有意思：
[CSS float浮动的深入研究、详解及拓展(一)](http://www.zhangxinxu.com/wordpress/?p=583)，[CSS float浮动的深入研究、详解及拓展(二)](http://www.zhangxinxu.com/wordpress/?p=594)。

总结下有如下可以学习的知识点。

1. 浮动的出现的意义：**文字环绕图片**。
2. 浮动的本质：”包裹和破坏“。
    *  ”包裹“——浮动就是个**带有方位的`display；inline-block`属性**。`display:inline-block` 具有包裹的作用，元素被包裹之后其宽度自适应元素本身大小;`float:left`或者`float:right`某种程度上等价于`display:inline-block`，其唯一区别在于：`float`具有方向性,`display:inline-block`仅仅有一个水平方向排列，而`float`可以从左到右排列，还可以从右到左排列（很少用到，没有多大意义）。
    * ”破坏性“，如上所述，浮动的意义是**让文字环绕图片**，而这时由于`float`**破坏了正常的line boxes**。

 例如在`<q>这只是一个普通的标签，这里有一个<cite>cite</cite>标签</q>`中有四种boxes
 containing box->line boxes->inline boxes(包括匿名的，不会成块显示，而是排成一行)->content area
如图所示：
 <img  alt="line boxes示意" src="http://paddingme.qiniudn.com/float.png" >


CSS中关于高度,[文中](http://www.zhangxinxu.com/wordpress/?p=583)也给出了很好的介意：
>在目前的CSS的世界中，所有的高度都是有两个CSS模型产生的，一个是box盒状模型，对应CSS为”height+padding+margin”，另外一个是line box模型，对应样式为”line-height”。前者的height属性分为明显的height值和隐藏的height值，所谓隐藏的height值是指图片的高度，一旦载入一张图片，其内在的height值就会起作用，即使您看不到”height”这个词。而后者针对于文字等这类inline boxes的元素（图片也属于inline boxes，但其height比line-height作用更凶猛，故其inline boxes高度等于其自身高度，对line-height无反应），inline boxes的高度直接受line-height控制（改变line-height文字拉开或重叠就是这个原因），而真正的高度表现则是由每行众多的inline boxes组成的line boxes（等于内部最高的inline box的高度），而这些line boxes的高度垂直堆叠形成了containing box的高度，也就是我们见到的div或是p标签之类的高度了。

浮动破坏了图片的inline-box，导致文字和图片无法同行显示，脱离了原来的line-box链，也没有了高度（无inline-box高度->无line-box高度-无高度）而这些结果导致了文字环绕图片显示。
[http://image.zhangxinxu.com/flash/blog/201001/css_float_by_zhangxinxu.swf](http://image.zhangxinxu.com/flash/blog/201001/css_float_by_zhangxinxu.swf) 中有很容易理解的动画显示。

“包裹与破坏”！包裹是让标签占据的空间水平收缩，破坏是破坏的inline box。inline boxes是高度形成的基础，浮动破坏了inline boxes也就没有高度可言了。真是由于浮动元素没有了inline boxes，没有了inline boxes高度，才能让其他inline boxes元素重新整合，环绕浮动元素排列。


浮动定位于绝对定位的区别：绝对定位元素也具有包裹性，绝对定位的元素脱离了文档流而浮动元素仍然在文档流中，这造成的差异是：同处于文档流中的 文字不会与浮动元素造成重叠，而会与绝对定位元素重叠


浮动使高度塌陷->清楚浮动！
塌陷原因：元素含有浮动属性->破坏inline-box高度->破坏line-box高度->无高度

清除浮动：

1. `<div style="clear:both;"></div>`:浪费一个div标签
2.  `.fix{voerflow:hidden;zoom:1}`:overflow:hidden;如果里面的元素要是想来个margin负值定位或是负的绝对定位，则会直接被裁掉了，所以此方法有局限性的。
3. `.fix{zoom:1;}.fix:after{display:block; content:'clear'; clear:both; line-height:0; visibility:hidden;}`

以上皆来自张鑫旭-鑫空间-鑫生活[http://www.zhangxinxu.com](http://www.zhangxinxu.com)






