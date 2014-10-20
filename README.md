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
