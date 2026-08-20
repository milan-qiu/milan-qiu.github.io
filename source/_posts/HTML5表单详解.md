---
title: "HTML5表单详解"
date: "2020-04-12 17:27:00"
tags:
categories:
description: >-
  input 1、type = “file”时，form标签要添加 enctype = "multipart/form-data" 2、含有required时，但是form有novalidate，那么required不会生效 3、含有required时，submit提交按钮含有formnovalida
---

<h2>input</h2>
<p>1、<strong>type = &ldquo;file&rdquo;</strong>时，form标签要添加 <strong>enctype = "multipart/form-data"</strong></p>
<p>&nbsp;</p>
<p>2、含有<strong>required</strong>时，但是form有<strong>novalidate</strong>，那么required不会生效</p>
<p>3、含有<strong>required</strong>时，submit提交按钮含有<strong>formnovalidate</strong>属性，那么reuired不会生效</p>
<p>&nbsp;</p>
<p>4、含有<strong>autofocus</strong>时，刷新页面时自动聚焦到该文本框上</p>
<p>5、含有<strong>autocomplete</strong>时，会记住之前提交的记录，利与快速填写</p>
<p>6、含有<strong>pattern</strong>属性时，要符合pattern的正则表达式才能提交。如 pattern = "[abc]$"，以abc任意一个字母结尾</p>
<p>&nbsp;</p>
<p>7、<strong>lable中的for</strong>，对应input的id值。当鼠标点击lable标签时，焦点就会在对应的input里面。（最佳搭配还是与radio、checkbox）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="text"</span> <span style="color: #0000ff;">/&gt;  &lt;</span><span style="color: #800000;">label </span><span style="color: #ff0000;">for</span><span style="color: #0000ff;">="text"</span><span style="color: #0000ff;">&gt;</span>一个label，配文本框<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>8、限制输入框最大长度：maxlength = "3"，限制输入框最小长度：minlength = "2"（效果不明显）。明显效果用：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="number"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="bb"</span><span style="color: #ff0000;"> oninput</span><span style="color: #0000ff;">="sub(this,5)"</span> <span style="color: #0000ff;">/&gt;   &lt;!-- 限制最大长度为5 --&gt;<br />&lt;!-- type可以各种各样 --&gt;</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span><span style="color: #000000;"> sub(obj,length){
    </span><span style="color: #0000ff;">if</span>(obj.value.length&gt;<span style="color: #000000;">length){
        obj.value </span>= obj.value.substr(0<span style="color: #000000;">,length);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>9、去除 type="search" 的默认小叉，</p>
<div class="cnblogs_code">
<pre>input [type="search"]::webkit-search-cancel-<span style="color: #000000;">button{
    </span>-webkit-appearance:none;    <span style="color: #008000;">//</span><span style="color: #008000;">去除默认小叉</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">若有需要可以自定义自己的小叉图标，如：</span>
<span style="color: #000000;">    width:15px;
    height:15px;
    background</span>-<span style="color: #000000;">color:red;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>10、type="number"时，保留两位小数用，step="0.01"。（若不设置，提交时自动去除小数点后的数）</p>
<p>11、type="number"时，点击右边的上下键，一次跳5，step="5"。（若不设置，默认跳1）</p>
<p>&nbsp;</p>
<p>12、去除type="number"的上下键，用：</p>
<div class="cnblogs_code">
<pre>input[type=number]::-webkit-inner-spin-<span style="color: #000000;">button,
input[type</span>=number]::-webkit-outer-spin-<span style="color: #000000;">button{
    </span>-webkit-<span style="color: #000000;">appearance:none;
    margin:</span>0<span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>HTML5约束验证API（validity）</h2>
<p>//每一个input都有与之对应的validity对象，如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="tt"</span><span style="color: #ff0000;"> required </span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>console.log(tt.validity);    <span style="color: #008000;">//</span><span style="color: #008000;">有id名的可以直接用id名使用，但兼容性没那么好</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>//打印出来的validity，如下：</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200412093039935-110562912.png" alt="" /></p>
<p>&nbsp;</p>
<p>//只要input设置了某些属性，与之对应的validity方法就会为true</p>
<p>&nbsp;</p>
<h2>HTML5约束验证API（checkValidity）</h2>
<p>//每个input都有checkValidity，只是检查规则随着type的不同而不同</p>
<p>//检查某类型是否符合规则，符合返回true，不符合返回false</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="email"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="emails"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span><span style="color: #000000;">(emails.checkValidity()){
    console.log(</span>"符合规则"<span style="color: #000000;">);
}</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
    console.log(</span>"不符合规则"<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>HTML5约束验证API（setCustomvalidity）</h2>
<p>//主要是更改input的required的提示信息，如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> pattern</span><span style="color: #0000ff;">="^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$"</span><span style="color: #ff0000;"> required oninput</span><span style="color: #0000ff;">="tishi(this)"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="submit"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span><span style="color: #000000;"> tishi(obj){
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;">(obj.validity.valueMissing){
        obj.setCustomValidity(</span>"这里不能为空空空。。。"<span style="color: #000000;">);
    }</span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;">(obj.validity.patternMismatch){
        obj.setCustomValidity(</span>"必须符合邮箱规则则则。。。"<span style="color: #000000;">);
    }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
        obj.setCustomValidity(</span>""<span style="color: #000000;">);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>HTML5自带验证美化</h2>
<h3>:required（选择必填项）</h3>
<div class="cnblogs_code">
<pre>input:reqrired{    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 选择input的必填项 </span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">
    border-right:3px solid red;
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>:optional（选择选填项）</h3>
<div class="cnblogs_code">
<pre>textarea:optional{ <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 指textarea没有required的那一项 </span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">
    border-right:3px solid grey;
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>去除默认的输入状态边框</h3>
<div class="cnblogs_code">
<pre>input:focus{  <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 去除input表单，光标进去后，默认的边框效果 </span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">
    outline:none;
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>自定义输入状态边框</h3>
<div class="cnblogs_code">
<pre>input:required:focus{ <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 设置输入状态的边框 </span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">
    box-shadow: 0 0 3px 1px red;
}</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>input:optional:focus{ <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 设置输入状态的边框 </span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">
    box-shadow: 0 0 3px 1px grey;
}</span></pre>
</div>
<h3>:valid（符合输入规则）</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> pattern</span><span style="color: #0000ff;">="^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$"</span><span style="color: #ff0000;"> required </span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="submit"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">/*</span><span style="color: #008000;"> 符合input的xx类型的规则时， </span><span style="color: #008000;">*/</span><span style="color: #000000;">
input:valid</span>~label::after{ <span style="color: #008000;">/*</span><span style="color: #008000;">获取同父级下面的lable</span><span style="color: #008000;">*/</span><span style="color: #000000;">
    content: </span>"ok符合规则"<span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>:invalid（不符合输入规则）</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="email"</span><span style="color: #ff0000;"> required </span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="submit"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">/*</span><span style="color: #008000;"> 不符合input的xx类型的规则时， </span><span style="color: #008000;">*/</span><span style="color: #000000;">
input:invalid</span>~label::after{ <span style="color: #008000;">/*</span><span style="color: #008000;">获取同父级下面的lable</span><span style="color: #008000;">*/</span><span style="color: #000000;">
    content: </span>"暂时不符合规则"<span style="color: #000000;">;
}</span></pre>
</div>
<h3>修改setCustomValidity的默认气泡</h3>
<p>......</p>
<p>&nbsp;</p>
