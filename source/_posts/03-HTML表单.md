---
title: "03-HTML表单"
date: "2020-01-18 10:29:00"
updated: "2020-01-18 10:31:00"
tags:
categories:
description: >-
  1、input表单输入元素，type属性，<input type=""> text：文字域 password：密码域 file：文件域 checkbox：复选域 radio：单选域 button：按钮 submit：提交按钮 reset：重置按钮 hidden：隐藏域 image：图像域 2、单选按
---

<p><strong><span style="font-family: 幼圆; font-size: 16px;">1、input表单输入元素，type属性，&lt;input type=""&gt;</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">text：文字域<br />
password：密码域

file：文件域

checkbox：复选域

radio：单选域

button：按钮

submit：提交按钮

reset：重置按钮

hidden：隐藏域

image：图像域</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>2、<strong>单选按钮（radio）</strong></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
nan</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="radio"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="sex"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="man"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//value不显示，但会发送到服务器
nv</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="radio"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="sex"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="woman"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//单选按钮name值必须一样
bm</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="radio"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="sex"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="bm"</span><span style="color: #ff0000;"> checked</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//checked开始值被选中
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">form标签中，实现表单元素的添加</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">input：表单输入标签

select：下拉菜单和列表标签

option：下拉菜单和列表项目分组标签

optgroup：下拉菜单和列表项目分成标签

textarea：文字域标签</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>3、<strong>复选框</strong></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
dushu</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="checkbox"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="1&Prime; value="</span><span style="color: #ff0000;">dushu"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//value不显示，但会发送到服务器
changge</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="checkbox"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="2&Prime; value="</span><span style="color: #ff0000;">changge"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;"> 　　//name值可以一样，也可以不一样
tiaowu</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="checkbox"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="3&Prime; value="</span><span style="color: #ff0000;">tiaowu"checked</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//checked开始值被选中
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>4、<strong>图像域</strong></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="image"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="4&Prime; src="</span><span style="color: #ff0000;">#"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//src是图像域必不可少的。图像域相当于提交按钮使用
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>5、<strong>隐藏域,target是链接打开的方式，_blank是从新的页面打开链接</strong></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form </span><span style="color: #ff0000;">target</span><span style="color: #0000ff;">="_blank"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="hidden"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//隐藏提交的内容
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>6、option<strong>下拉菜单，一次只能选择一个</strong></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">select </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> selected</span><span style="color: #0000ff;">&gt;</span>&ndash;请选择&ndash;<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//selected默认选项状态
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项二<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项三<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 16px; font-family: 幼圆;">select标签属性</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">name：设置下拉菜单和列表的名称

multiple：设置可选择多个选项

size：设置列表中可见选项的数目</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>7、<strong>一次显示3个，按ctrl可多选</strong></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">select </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> size</span><span style="color: #0000ff;">="3&Prime; multiple&gt;
&lt;option value="</span><span style="color: #ff0000;">"</span><span style="color: #0000ff;">&gt;</span>选项一<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项二<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项三<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>8、下拉菜单分组</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">optgroup </span><span style="color: #ff0000;">label</span><span style="color: #0000ff;">="组1&Prime;&gt;　　　//optgroup对选项进行分组，label是组名
&lt;option value="</span><span style="color: #ff0000;">" selected</span><span style="color: #0000ff;">&gt;</span>选项一<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;　　//</span><span style="color: #000000;">selected默认选项状态
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项二<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项三<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">optgroup</span><span style="color: #0000ff;">&gt;<br /><br /></span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">optgroup </span><span style="color: #ff0000;">label</span><span style="color: #0000ff;">="组2&Prime;&gt;
&lt;option value="</span><span style="color: #ff0000;">"</span><span style="color: #0000ff;">&gt;</span>选项一<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项二<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>选项三<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">optgroup</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">9、textarea文字域</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">textarea </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> rows</span><span style="color: #0000ff;">="5&Prime; cols="</span><span style="color: #ff0000;">50&Prime; placeholder</span><span style="color: #0000ff;">="请输入。。"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//rows是文本域的行数，cols是文本域的宽度
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">textarea</span><span style="color: #0000ff;">&gt;　　</span>//placeholder是文本域的提示信息</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>10、span标签：没有实际意义，只是为了应用样式</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;　　</span>span标签是是行内标签，里面添加的内容都在一行显示　　<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>11、div块级标签：可以包含行内标签，但行内标签不可以包含块级标签。</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;　　</span>div标签是块级标签，一个div占一行　　<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
