# 目录

## HTML & CSS 文章

1. [语义化](https://github.com/paddingme/Learning-HTML-CSS/blob/master/articles/semantic-html.md)
2. [使用HTML、CSS写好一个输入框](https://github.com/paddingme/Learning-HTML-CSS/blob/master/articles/input.md)
3. [form 表单的正确使用](https://github.com/paddingme/Learning-HTML-CSS/blob/master/articles/form.md)
4. [基本视觉格式化](https://github.com/paddingme/Learning-HTML-CSS/blob/master/articles/basic-visual-formatting.md)
4. [CSS 中的float标签](https://github.com/paddingme/Learning-HTML-CSS/blob/master/articlesfloat-label-in-css.md)
4. [浮动](https://github.com/paddingme/Learning-HTML-CSS/blob/master/float.md)
4. [HTML head 头标签](https://github.com/paddingme/Learning-HTML-CSS/blob/master/html-head-tags.md)
5. [学习CSS布局](https://github.com/paddingme/Learning-HTML-CSS/blob/master/learn-css-layout.md)
6. [模式？标准！](https://github.com/paddingme/Learning-HTML-CSS/blob/master/mode-or-standard.md)
7. [CSS中的值和单位、字体以及文本属性](https://github.com/paddingme/Learning-HTML-CSS/blob/master/value-unit-font-and-text-attribute-in-the-css.md)


---

## 知识碎片

### 1. `title` 属性 和 `alt` 属性

`title`的正确使用场景主要有以下四种：

- 链接-描述目标信息
- 图片-版权/描述
- 引用-来源信息
- 交互元素-操作指南

而 `alt` 属性为不能显示图像、窗体或applets的用户代理（UA），alt属性用来指定替换文字。替换文字的语言由lang属性指定。Alt属性（注意是“属性”而不是“标签”）包括替换说明，对于图像和图像热点是必须的。它只能用在img、area和input元素中（包括applet元素）。对于input元素，alt属性意在用来替换提交按钮的图片。比如：`<input type="image" src="image.gif" alt="Submit" />`。对于那些装饰性的图片可以使用空的值（alt=""，引号中间没有空格）

参考： [alt属性和title属性](http://www.junchenwu.com/2005/05/alttitle.html)

### 2. 清除浮动和闭合浮动的区别

原来是一丝提出的“闭合浮动”。为了避免混淆，还是说全吧，“使float元素可以撑高父元素”。

（国内页面重构已经足够乱了还需要特地造个新名词混淆新人吗）

“清除浮动”源于clear float即W3C CSS2.1 9.5.2章定义的内容，意即使用clear阻止这个元素盒子的边和前面的浮动元素相邻的行为；

> The most interesting characteristic of a float (or "floated" or "floating" box) is that content may flow along its side (or be prohibited from doing so by the 'clear' property).

如果“闭合浮动”指的是避免“float无法撑高父容器的默认行为”的话，那么有这些方案：

- 在float同级最后方加入带有clear:both属性的元素或伪元素（W3C CSS2.1 9.5.2 clearance高度计算部分）
- 给父级加上一些overflow/float/display table等触发BFC的属性以使父容器成为block formatting context roots（W3C CSS2.1 10.6.7）

>10.6.7 'Auto' heights for block formatting context roots
In addition, if the element has any floating descendants whose bottom margin edge is below the element's bottom content edge, then the height is increased to include those edges. Only floats that participate in this block formatting context are taken into account, e.g., floats inside absolutely positioned descendants or other floats are not.

参考:<http://segmentfault.com/q/1010000000732608>

### 3. label 标签的应用

 ```
 <input id="J_MyChk" type="checkbox" value="">
 <label for="J_MyChk">点击我也可以让左边选中</label>
 ```

 ```
 <label><input type="checkbox" value="">点击我也可以让左边选中</label>
 ```

### 4. `<button type="button">我是一个按钮</button>`












