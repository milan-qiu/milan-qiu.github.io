---
title: "08-JS DOM事件"
date: "2020-01-22 17:31:00"
tags:
categories:
description: >-
  鼠标事件类型 click：当用户点击某个对象时调用的事件句柄。 dbclick：当用户双击某个对象时调用的事件句柄。 mousedown：鼠标按钮被按下。 mouseup：鼠标按键被松开 mouseover：鼠标移到某元素之上 //进入它的子元素也会触发 mouseout：鼠标从某元素移开 //进入
---

<p><span style="font-size: 18pt;"><strong>&nbsp;</strong></span></p>
<p><span style="font-size: 18pt; font-family: 幼圆;"><strong>鼠标事件类型</strong></span></p>
<div class="cnblogs_code">
<pre><span>click：当用户点击某个对象时调用的事件句柄。
dbclick：当用户双击某个对象时调用的事件句柄。
 
mousedown：鼠标按钮被按下。
mouseup：鼠标按键被松开

mouseover：鼠标移到某元素之上    //进入它的子元素也会触发<span>
mouseout：鼠标从某元素移开      //进入它的子元素也会触发<span>

mouseenter：鼠标移到某元素之上     //不包括它的子元素<span>
mouseleave：鼠标从某元素移开      //不包括它的子元素
<span>
mousemove：鼠标在某元素移动。</span></span></span></span></span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 18pt;">HTML事件</span></strong></p>
<div class="cnblogs_code">
<pre>//在html绑定，在类型前加"on"HTML部分：&lt;button  onclick=&rdquo;qq(<span style="color: #0000ff;">this</span>)&rdquo;&gt; 开始 &lt;/button&gt;    //this可以把自身发送到qq函数去

<span style="color: #0000ff;"><span style="color: #000000;">JavaScript部分：</span> function</span>  qq (abc){  }    <span style="color: #008000;">//</span><span style="color: #008000;">接收到的abc就是整个button本身</span>
<span style="color: #000000;">
注：函数用this指向button本身，这样函数体就不用用id等方式获取dom元素了，有发送就得接收，函数function qq (abc)，可以用abc等接收


script要放在head里面时，用
window.onload</span>=<span style="color: #0000ff;">function</span>(){}    <span style="color: #008000;">//</span><span style="color: #008000;">页面加载完之后再加载该脚本</span>
<br /><br /><br />获取select下拉框的值，两种方法</pre>
<p>　//var a = this.value;</p>
<p>　//var a = menu.options[menu.selectedIndex].value;&nbsp; &nbsp;//menu为select菜单的id值</p>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 18pt;">DOM0级事件</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">（在js绑定）

如：</span>&lt;button  id=&rdquo;qml&rdquo; class=&rdquo;kk&rdquo;&gt;开始&lt;/button&gt;

<span style="color: #0000ff;">var</span> qml =<span style="color: #000000;"> document.getElementById(&ldquo;qml&rdquo;);

qml.onclick </span>= <span style="color: #0000ff;">function</span>(){         <span style="color: #008000;">//</span><span style="color: #008000;">给qml的button绑定一个点击事件，点击触发匿名函数</span>

<span style="color: #0000ff;">this</span>.className = &ldquo;jj&rdquo;;       <span style="color: #008000;">//</span><span style="color: #008000;">用this指向，把原来kk的类名换成jj</span>
<span style="color: #000000;">
}</span>&nbsp;</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆;"><strong><span style="font-size: 18pt;">键盘事件类型</span></strong></span></p>
<div class="cnblogs_code">
<pre>keypress：某个键盘按键被按下并松开。//keypress 搭配 event.charCode 比较稳定。charCode返回ascll码
<span>
keydown：某个键盘按键被按下。

keyup：某个键盘按键被松开。<br /><br />//如：document.onkeyup = function() {}&nbsp; &nbsp;//键盘按键松开时触发函数<br /></span></pre>
</div>
