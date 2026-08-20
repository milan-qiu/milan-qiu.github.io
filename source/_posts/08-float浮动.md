---
title: "08-float浮动"
date: "2020-01-18 12:28:00"
tags:
categories:
description: >-
  float（浮动） left：左浮动 right：右浮动 清除浮动方法一 .clear{ clear:both;} <div class = "clear"> </div> //浮动元素后使用一个空元素 清除浮动方法二 overflow:hidden; //给浮动元素的父级添加 zoom:1; //
---

<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">float（浮动）</span></strong></p>
<p>&nbsp;</p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">left：左浮动
right：右浮动
</pre>
</div>
<p>&nbsp;</p>
<p>　　</p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">清除浮动方法一</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.clear{ clear:both;}
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class </span><span style="color: #0000ff;">= "clear"</span><span style="color: #0000ff;">&gt;</span> <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;　　</span>//浮动元素后使用一个空元素</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>清除浮动方法二</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">overflow:hidden;　　//给浮动元素的父级添加
zoom:1;　　//低版本ie浏览器兼容性</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">清除浮动方法三</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.className:after{
content: ".";　　//另内容为空
display: block;　　//转换为一个块元素
height: 0;
visibility: hidden;　　//隐藏显示
clear: both;　　//清除浮动，通常把这个写到下一个不需要浮动的块级元素里
}
.className{
zoom:1;//低版本ie浏览器兼容性
}</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;">其他方法</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">1、给父级元素定义height<br />
2、父级元素也一起浮动（会产生新的浮动问题）<br /></span></pre>
</div>
