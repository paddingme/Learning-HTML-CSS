# `form` 表单的正确使用

- [form提交的几种方法](http://suo.iteye.com/blog/493998)
- [form表单](http://www.w3cplus.com/framework/page/form.php)
- [onsubmit阻止form表单提交与onclick的相关操作](http://www.jb51.net/article/24709.htm)


# [form提交的几种方法](http://suo.iteye.com/blog/493998)

## 方法一：利用form的onsubmit()函数

```
<script>
    function validateForm(){
        if(document.reply.title.value == ""){ //通过form名来获取form
        alert("please input the title!");
        document.reply.title.focus();
        return false;
    }

    if(document.forms[0].cont.value == ""){ //通过forms数组获取form
        alert("please input the content!");
        document.reply.cont.focus();
        return false;
    }
    return true;
  }
</script>

<form name="reply"  method="post" onsubmit="return validateForm( );">
        <input type="text" name="title"  size="80" /><br />
        <textarea name="cont" cols="80" rows="12"></textarea><br />
        <input type="submit" value="提交" >
</form>

```

注意：
1.onsubmit属性内容一定要有return关键字，否则函数会直接执行，不会返回
2.validateForm一定要返回一个boolean类型的返回值
3.提交按钮要写成submit类型的

## 方法二：利用input类型为submit组件的onclick()函数
 1. 将上面form标签中的onsubmit="return validateForm()"属性，去掉。
 2. 为“提交”按钮添加onclick事件，如下：

    <input type="submit" value="提交" onclick="return validateForm();">

## 方法三：利用button组件的onclick()函数，手动提交

```
<script>
    function modifyItem() {
        if (trim(document.getElementById("itemName").value) == "") {
            alert("物料名称不能为空！");
            document.getElementById("itemName").focus();
            return;
        }
        with (document.getElementById("itemForm")) {
            method = "post";
            action = "item.do?command=modify&pageNo=${itemForm.pageNo}";
            submit();
        }
    }
    //返回
    function goBack() {
        window.self.location = "item.do?command=list&pageNo=${itemForm.pageNo}";
    }
</script>
<form name="itemForm" id="itemForm">
      <input name="itemNo" type="text"   id="itemNo" value="${ item.itemNo }" >
      <input name="itemName" type="text"   id="itemName" value="${ item.itemName }" >
     <input name="btnModify"  type="button" id="btnModify" value=“修改" onclick="modifyItem()">
</form>
```

注意：
 1.提交时，设置form的action和methods属性，然后利用form.submit()函数提交。

## 总结：
 1. 对form中的组件验证时，前两个使用的是name属性，包括form自身的。
 2. 如果提交表单时没有反应，同时确定提交表单部分代码没有问题，请查看提交表单前面的js代码，有时前面js的错误会引发莫名其妙的问题。

```
<!DOCTYPE html>
<html lang="zh-cmn-Hans">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        @charset "utf-8";
/* -------------------------------------------------
 * form
 * -------------------------------------------------
*/
form{
    margin-bottom:18px;
    font-size:13px;
}
textarea {
    resize:none;
    vertical-align:top;
    overflow:auto;
    font:12px/1.5 Helvetica,Arial,sans-serif;
    width:500px;
    height:80px;
}
.form-text{
    margin:0;
    font:12px/1.5 Helvetica,Arial,sans-serif;
    height:18px;
    width:200px;
}
.form-text, textarea, select{
    border: 1px solid #CCCCCC;
    border-radius: 3px 3px 3px 3px;
    padding:4px;
}
.form-text, textarea {
  -webkit-transition: border linear 0.2s, box-shadow linear 0.2s;
  -moz-transition: border linear 0.2s, box-shadow linear 0.2s;
  -ms-transition: border linear 0.2s, box-shadow linear 0.2s;
  -o-transition: border linear 0.2s, box-shadow linear 0.2s;
  transition: border linear 0.2s, box-shadow linear 0.2s;
  -webkit-box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  -moz-box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
}
.form-text:focus, textarea:focus,select{
    outline: 0 none;
}
.form-text:focus, textarea:focus {
  border-color: rgba(82, 168, 236, 0.8);
  -webkit-box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1), 0 0 8px rgba(82, 168, 236, 0.6);
  -moz-box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1), 0 0 8px rgba(82, 168, 236, 0.6);
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1), 0 0 8px rgba(82, 168, 236, 0.6);
}
.form-radio,.form-checkbox{
    margin:0;
    padding:0;
    width:13px;
    height:13px;
    font-size:13px;
}
:-moz-placeholder,
::-webkit-input-placeholder{
  color: #bfbfbf;
}
/* form-item */
.form-item{
    margin-bottom:9px;
}
/* horizontal form label */
.form-horizontal label{
    float: left;
    text-align: right;
    font-weight:500;
    width:100px;
    font-size:12px;
    line-height:19px;
}
.form-horizontal .form-field{
    float:left;
}
.form-horizontal .form-action,
.form-horizontal .item-no-label{
    padding-left:100px;/*label width*/
}
/* vertical form label */
.form-vertical label{
    display:block;
    float:none;
    width:auto;
    text-align:left;
    margin-bottom:5px;
}
.form-vertical .form-field{
    float:none;
}
.form-vertical .form-action,
.form-vertical .item-no-label{
    padding-left:0;
}
/* field-list */
.form-radio-checkbox-wrap .form-field label{
    text-align: left;
    width: auto;
    font-weight:normal;
    margin:0 10px 0 0;
    float:left;
    display:inline;
}
.form-radio-checkbox-wrap .form-field .field-list-block{
    display:block;
    float: none;
    margin-right:0;
    overflow:auto;*zoom:1;
}
.form-radio-checkbox-wrap .form-radio,
.form-radio-checkbox-wrap .form-checkbox,
.form-radio-checkbox-wrap span{
    float:left;
    display:inline;
}
.form-radio-checkbox-wrap .form-radio,
.form-radio-checkbox-wrap .form-checkbox{
    margin-right:5px;
    margin-top:3px;
}
/* form-action */
.form-action{
    clear:both;
}
.submit-wrap{
    -moz-border-radius:5px;
    -webkit-border-radius:5px;
    border-radius:5px;
    display:inline-block;*display:inline;*zoom:1;
}
.submit-btn{
    border: 0 none;
    height:26px;
    margin:0;
    background:none;
    overflow:visible;
    padding:0 10px;
    cursor:pointer;
}
@-moz-document url-prefix(){
    .submit-btn{
        padding-bottom:3px;
    }
}
/* description */
.form-des{
    color: #bfbfbf;
    font-size:12px;
    margin-left:5px;
}
p.form-des{
    margin:0;
}
/* codePic */
.code-pic{
    display:inline-block;*display:inline;*zoom:1;
}
.code-pic img{
    height:28px;
    vertical-align:middle;
    margin:0 5px;
}
/* tips messages */
.form-error, .form-alert, .form-notice, .form-success, .form-info {
    border: 2px solid #DDDDDD;
    margin-bottom: 9px;
    padding:8px;
    font-size:12px;
}
/* span inline tips */
span.form-error, span.form-alert, span.form-notice, span.form-success, span.form-info {
    border-width:1px;
    display:inline-block;*display:inline;*zoom:1;
    line-height:26px;
    vertical-align:middle;
    padding:0 5px;
    font-size:12px;
    margin:0 0 0 5px;
}
.form-error, .form-alert {
    background: none repeat scroll 0 0 #FBE3E4;
    border-color: #FBC2C4;
    color: #8A1F11;
}
.form-notice {
    background: none repeat scroll 0 0 #FFF6BF;
    border-color: #FFD324;
    color: #514721;
}
.form-info {
    background: none repeat scroll 0 0 #D5EDF8;
    border-color: #92CAE4;
    color: #205791;
}
.form-success {
    background: none repeat scroll 0 0 #E6EFC2;
    border-color: #C6D880;
    color: #264409;
}
.form-error a, .form-alert a,.form-notice a,.form-info a,.form-success a{
    text-decoration:underline;
}
.form-error a, .form-alert a {
    color: #8A1F11; 
}
.form-notice a {
    color: #514721;
}
.form-info a {
    color: #205791;
}
.form-success a {
    color: #264409;
}
/* clear form-item float */
.form-item:before, .form-item:after {
    content:"";
    display:table;
}
.form-item:after{
    clear:both;
    overflow:hidden;
}
.form-item{
    zoom:1;
    clear:both;
    margin-bottom:9px;
}
    </style>
</head>

<body>
    <h3>label同行表单demo</h3>
    <section class="demozone">
        <form class="demo form-horizontal" id="demo2" action="#" method="post">
            <div class="form-item">
                <label for="username">昵称：</label>

                <div class="form-field">
                    <input type="text" name="username" id="username" class="form-text" placeholder="6-32个字符" />
                </div>
            </div>
            <div class="form-item">
                <label for="name">邮箱：</label>

                <div class="form-field">
                    <input type="email" name="email" id="email" class="form-text" />
                </div>
            </div>
            <div class="form-item">
                <label for="pwd">密码：</label>

                <div class="form-field">
                    <input type="password" class="form-text" id="pwd" name="pwd">
                </div>
            </div>
            <div class="form-item form-radio-checkbox-wrap">
                <label>性别：</label>

                <div class="form-field">
                    <label>
                        <input type="radio" name="sex" class="form-radio" value="man" checked="checked">
                        <span>男</span>
                    </label>
                    <label>
                        <input type="radio" name="sex" class="form-radio" value="woman">
                        <span>女</span>
                    </label>
                </div>
            </div>
            <div class="form-item form-radio-checkbox-wrap">
                <label>Options：</label>

                <div class="form-field">
                    <label class="field-list-block">
                        <input type="checkbox" checked="checked" value="1" class="form-checkbox" name="">
                        <span>Option one is this and that—be sure to include why it’s great</span>
                    </label>
                    <label class="field-list-block">
                        <input type="checkbox" value="2" class="form-checkbox" name="">
                        <span>Option two can also be checked and included in form results</span>
                    </label>
                    <label class="field-list-block">
                        <input type="checkbox" value="3" class="form-checkbox" name="">
                        <span>Option three can—yes, you guessed it—also be checked and included in form results</span>
                    </label>
                </div>
            </div>
            <div class="form-item">
                <label for="realname">姓名：</label>

                <div class="form-field">
                    <input type="text" name="realname" id="realname" class="form-text" placeholder="请填入真实姓名" />
                </div>
            </div>
            <div class="form-item">
                <label>证件号码：</label>

                <div class="form-field form-id-num-wrap">
                    <select id="id_type" size="1" name="id_type">
                        <option value="1" selected="selected">身份证</option>
                        <option value="2">学生证</option>
                        <option value="3">军官证</option>
                    </select>
                    <input type="text" name="id_text" id="id_text" class="form-text" />
                </div>
            </div>
            <div class="form-item">
                <label>个人简介：</label>

                <div class="form-field">
                    <textarea name="intro" id="intro"></textarea>

                    <p class="form-des">说明注释文字可以放在这里啊</p>
                </div>
            </div>
            <div class="form-item">
                <label for="codetext">验证码：</label>

                <div class="form-field form-code-text-wrap">
                    <input type="text" id="codetext" name="codetext" class="form-text code-text">

                    <div class="code-pic">
                        <img id="codePic" alt="" src="http://www.w3cplus.com/solution/form/images/code.jpg"><a id="change_code" href="#">换一个</a>
                    </div>
                </div>
            </div>
            <div class="form-item item-no-label form-radio-checkbox-wrap">
                <div class="form-field">
                    <label>
                        <input type="checkbox" name="" class="form-checkbox" value="1" checked="checked">
                        <span>我同意所有条款……</span>
                    </label>
                </div>
            </div>
            <div class="form-action">
                <span class="submit-wrap greybtn">
                    <input type="submit" value="提交" class="submit-btn">
                </span>
            </div>
        </form>
    </section>
    <h3>label换行表单</h3>
    <section class="demozone">
        <form method="post" action="#" id="demo3" class="demo form-vertical">
            <div class="form-item">
                <label for="username">昵称：</label>

                <div class="form-field">
                    <input type="text" placeholder="6-32个字符" class="form-text" id="username" name="username">
                </div>
            </div>
            <div class="form-item">
                <label for="name">邮箱：</label>

                <div class="form-field">
                    <input type="email" class="form-text" id="email" name="email">
                </div>
            </div>
            <div class="form-item">
                <label for="pwd">密码：</label>

                <div class="form-field">
                    <input type="password" name="pwd" id="pwd" class="form-text">
                </div>
            </div>
            <div class="form-item form-radio-checkbox-wrap">
                <label>性别：</label>

                <div class="form-field">
                    <label>
                        <input type="radio" checked="checked" value="man" class="form-radio" name="sex">
                        <span>男</span>
                    </label>
                    <label>
                        <input type="radio" value="woman" class="form-radio" name="sex">
                        <span>女</span>
                    </label>
                </div>
            </div>
            <div class="form-item form-radio-checkbox-wrap">
                <label>Options：</label>

                <div class="form-field">
                    <label class="field-list-block">
                        <input type="checkbox" checked="checked" value="1" class="form-checkbox" name="">
                        <span>Option one is this and that—be sure to include why it’s great</span>
                    </label>
                    <label class="field-list-block">
                        <input type="checkbox" value="2" class="form-checkbox" name="">
                        <span>Option two can also be checked and included in form results</span>
                    </label>
                    <label class="field-list-block">
                        <input type="checkbox" value="3" class="form-checkbox" name="">
                        <span>Option three can—yes, you guessed it—also be checked and included in form results</span>
                    </label>
                </div>
            </div>
            <div class="form-item">
                <label for="realname">姓名：</label>

                <div class="form-field">
                    <input type="text" placeholder="请填入真实姓名" class="form-text" id="realname" name="realname">
                </div>
            </div>
            <div class="form-item">
                <label>证件号码：</label>

                <div class="form-field form-id-num-wrap">
                    <select name="id_type" size="1" id="id_type">
                        <option selected="selected" value="1">身份证</option>
                        <option value="2">学生证</option>
                        <option value="3">军官证</option>
                    </select>
                    <input type="text" class="form-text" id="id_text" name="id_text">
                </div>
            </div>
            <div class="form-item">
                <label>个人简介：</label>

                <div class="form-field">
                    <textarea id="intro" name="intro"></textarea>

                    <p class="form-des">说明注释文字可以放在这里啊</p>
                </div>
            </div>
            <div class="form-item">
                <label for="codetext">验证码：</label>

                <div class="form-field form-code-text-wrap">
                    <input type="text" class="form-text code-text" name="codetext" id="codetext">

                    <div class="code-pic">
                        <img src="http://www.w3cplus.com/solution/form/images/code.jpg" alt="" id="codePic"><a href="#" id="change_code">换一个</a>
                    </div>
                </div>
            </div>
            <div class="form-item item-no-label form-radio-checkbox-wrap">
                <div class="form-field">
                    <label>
                        <input type="checkbox" checked="checked" value="1" class="form-checkbox" name="">
                        <span>我同意所有条款……</span>
                    </label>
                </div>
            </div>
            <div class="form-action">
                <span class="submit-wrap greybtn">
                    <input type="submit" value="提交" class="submit-btn">
                </span>
            </div>
        </form>
    </section>
    <h2>附加：状态提示信息的class</h2>

    <div class="demozone">
        <div class="form-error">This is a &lt;div&gt; with the class
            <strong>.form-error</strong>. <a href="#">Link</a>.
        </div>
        <div class="form-notice">This is a &lt;div&gt; with the class
            <strong>.form-notice</strong>. <a href="#">Link</a>.
        </div>
        <div class="form-info">This is a &lt;div&gt; with the class
            <strong>.form-info</strong>. <a href="#">Link</a>.</div>
        <div class="form-success">This is a &lt;div&gt; with the class
            <strong>.form-success</strong>. <a href="#">Link</a>.
        </div>
    </div>
    </article>
</body>

</html>
```
