---
title: "04、jQuery扩展"
date: "2020-03-14 12:32:00"
tags:
categories:
description: >-
  自定义动画 动画DOM及其CSS操作 原理：我们只需要以固定的时间间隔（例如，0.1秒），每次DOM元素的CSS样式修改一点（例如，高宽各增加10%），看起来就像动画了 animate({ }, time) //实现任意动画效果 // { }里面写最终效果(DOM元素的CSS样式)；time表示时间
---

<h2>自定义动画</h2>
<h3>动画DOM及其CSS操作</h3>
<p>原理：我们只需要以固定的时间间隔（例如，0.1秒），每次DOM元素的CSS样式修改一点（例如，高宽各增加10%），看起来就像动画了</p>
<p>&nbsp;</p>
<h3>animate({ }, time)&nbsp; &nbsp; &nbsp; &nbsp; //实现任意动画效果</h3>
<p>// { }里面写最终效果(DOM元素的CSS样式)；time表示时间，毫秒为单位，1秒 = 1000毫秒。如：</p>
<div class="cnblogs_code">
<pre>$('#dd'<span style="color: #000000;">).animate({
opcity:</span>0.5<span style="color: #000000;">,
width : </span>'100px'<span style="color: #000000;">,
height: </span>'100px'<span style="color: #000000;">
} , </span>3000 );              <span style="color: #008000;">//</span><span style="color: #008000;">3秒内，宽高都变成100px，透明度为50%</span></pre>
</div>
<p>&nbsp;</p>
<h3>delay()&nbsp; &nbsp; &nbsp; //实现动画暂停</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span><span style="color: #000000;"> dh(){
$(</span>'div').stop()        <span style="color: #008000;">//</span><span style="color: #008000;">停止当前div正在运行的动画</span>
.animation( {'width' : '0%'} , 1000<span style="color: #000000;"> )
.delay(</span>1000)          <span style="color: #008000;">//</span><span style="color: #008000;">动画暂停1秒钟</span>
.animation( {'width' : '100%'} , 1000<span style="color: #000000;"> );
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>stop()&nbsp; &nbsp; &nbsp; //停止当前正在运行的动画</h3>
<div class="cnblogs_code">
<pre>$('div').stop();     <span style="color: #008000;">//</span><span style="color: #008000;">停止当前div正在运行的动画</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>动画函数</h2>
<h3>显示/隐藏效果</h3>
<p><strong>show/hide()</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">直接以 无参形式调用show() 和 hide()，会显示和隐藏DOM元素，但是只要传递一个时间参数进去，竟会变成了动画</span>
<span style="color: #000000;">
$(</span>'#dd').show(3000);      <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐显示</span>
<span style="color: #000000;">
$(</span>'#dd').hide(3000);        <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐隐藏</span></pre>
</div>
<p><strong>toggle()</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">如果动画为show，执行toggle变成hide；如果动画为hide，执行toggle变成show</span>
<span style="color: #000000;">
$(</span>'#dd').toggle(3000);      <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐  隐藏/显示</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>淡入淡出效果</h3>
<p><strong>fadeIn/fadeOut()</strong></p>
<div class="cnblogs_code">
<pre>$('#dd').fadeIn(3000);      <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐  淡入（出现）</span>
<span style="color: #000000;">
$(</span>'#dd').fadeOut(3000);       <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐   淡出（隐藏）</span></pre>
</div>
<p><strong>fadeToggle()</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">如果动画为fadeIn，执行fadeToggle变成fadeOut；如果动画为fadeOut，执行fadeToggle变成fadeIn</span>
<span style="color: #000000;">
$(</span>'#dd').fadeToggle(3000);       <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐   淡入/淡出</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>上卷下拉效果</h3>
<p><strong>slideUp/slideDown()</strong>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;//在垂直方向逐渐展开或收缩</p>
<div class="cnblogs_code">
<pre>$('#dd').slideUp(3000);      <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐  往上收缩（隐藏）</span>
<span style="color: #000000;">
$(</span>'#dd').slideDown(3000);      <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐  往下展开（显示）</span></pre>
</div>
<p><strong>slideToggle()</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">如果动画为slideUp，执行slideToggle变成slideDown；如果动画为slideDown，执行slideToggle变成slideUp</span>
<span style="color: #000000;">
$(</span>'#dd').slideToggle(3000);       <span style="color: #008000;">//</span><span style="color: #008000;">该div 三秒内逐渐   上卷/下拉</span></pre>
</div>
<p>&nbsp;</p>
<h2>计时器（建议js原生）</h2>
<p>setTimeout</p>
<p>setInterval</p>
