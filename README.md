1. 使用HTML、CSS写好一个输入框

  如何做到输入框无无文字时和输入文字时一致对齐？  
  chrome 浏览器的输入框光标、输入文字、占位符有以下规则：
  - 无文字输入时，以行高为准；
  - 有文字输入时，以文字大小为准；
  - 占位符以行高为准。

  那么如何写好一个输入框：
  1. 在书写输入框的时候，如果要增加光标高度，那么最可行的做法是增加文字的大小;
  2. 输入框的剩余空白使用内边距填充；
  3. 不要为输入框设置行高，因为浏览器默认会设置行高就会使占位符和输入光标、文字都居中；
  4. 不要为输入框设置高度，因为已经使用了内边距撑开了，并且现在大多数 css 库都直接使用边框盒模型。

    ```
    <!DOCTYPE html>
    <style>
        body{
            line-height: 20px;
        }

        #input1{
            font-size: 40px;
            padding: 10px;
            line-height: normal;
        }
    </style>
    <body>
        <input type="text" id="input1" placeholder="input">
    </body>
    ```

    demo: <http://codepen.io/paddingme/pen/cJGhl>

    相关链接：<http://qianduanblog.com/post/css-learning-21-using-html-css-write-an-input-box.html>


2.  label 标签的应用

 ```
 <input id="J_MyChk" type="checkbox" value=""><label for="J_MyChk">点击我也可以让左边选中</label>
 ```

 ```
 <label><input type="checkbox" value="">点击我也可以让左边选中</label>
 ```

3. `<button type="button">我是一个按钮</button>`

4. `form `表单的正确使用

  https://github.com/paddingme/fex/issues/3

5. `title` 属性 和 `alt` 属性

 `title`的正确使用场景主要有以下四种：

 - 链接-描述目标信息
 - 图片-版权/描述
 - 引用-来源信息
 - 交互元素-操作指南

 而 `alt` 属性为不能显示图像、窗体或applets的用户代理（UA），alt属性用来指定替换文字。替换文字的语言由lang属性指定。Alt属性（注意是“属性”而不是“标签”）包括替换说明，对于图像和图像热点是必须的。它只能用在img、area和input元素中（包括applet元素）。对于input元素，alt属性意在用来替换提交按钮的图片。比如：`<input type="image" src="image.gif" alt="Submit" />`。对于那些装饰性的图片可以使用空的值（alt=""，引号中间没有空格）


 参考： [alt属性和title属性](http://www.junchenwu.com/2005/05/alttitle.html)
