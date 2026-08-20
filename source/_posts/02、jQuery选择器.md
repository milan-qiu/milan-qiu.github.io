---
title: "02、jQuery选择器"
date: "2020-03-14 12:18:00"
tags:
categories:
description: >-
  基本选择器 通配符选择器：var all = $('*'); //根据 $('*') 获取。 元素选择器：var ele = $('div'); //根据 $('元素名') 获取。如果给好几个元素绑定点击事件，$(this).index()可以确认点击的是第几个元素。 类选择器：var cla =
---

<h2>基本选择器</h2>
<div class="cnblogs_code">
<pre>通配符选择器：<span style="color: #0000ff;">var</span> all = $('*');  <span style="color: #008000;">//</span><span style="color: #008000;">根据   $('*')   获取。</span>
<span style="color: #000000;">
  元素选择器：</span><span style="color: #0000ff;">var</span> ele = $('div');   <span style="color: #008000;">//</span><span style="color: #008000;">根据   $('元素名')   获取。如果给好几个元素绑定点击事件，$(this).index()可以确认点击的是第几个元素。</span>
<span style="color: #000000;">
    类选择器：</span><span style="color: #0000ff;">var</span> cla = $('.bb');   <span style="color: #008000;">//</span><span style="color: #008000;">根据   $('.类名')   获取。</span>
<span style="color: #000000;">
   id选择器 ：</span><span style="color: #0000ff;">var</span> iid = $('#idname');   <span style="color: #008000;">//</span><span style="color: #008000;">根据   $('#id名')   获取</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>群组选择器：<span style="color: #0000ff;">var</span> duo = $('#dd, .aa');   <span style="color: #008000;">//</span><span style="color: #008000;">可根据多个不同的选择器，一起选择起来</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>后代选择器：<span style="color: #0000ff;">var</span> hou = $('div p');   <span style="color: #008000;">//</span><span style="color: #008000;">选择div里面的p元素</span>
<span style="color: #000000;">
  子选择器：</span><span style="color: #0000ff;">var</span> zi = $('div&gt;p');   <span style="color: #008000;">//</span><span style="color: #008000;">选择div的子代p元素，不会选择孙代p元素</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>相邻兄弟选择器：<span style="color: #0000ff;">var</span> xiong = $('.gg+div');   <span style="color: #008000;">//</span><span style="color: #008000;">选择紧邻 .dd 后的，一个div兄弟。注：如果.dd有多个，则可能有多个紧邻的兄弟。</span>
<span style="color: #000000;">
通用兄弟选择器：</span><span style="color: #0000ff;">var</span> txiong = $('.gg~div');   <span style="color: #008000;">//</span><span style="color: #008000;">选择 .dd 后的，所有div兄弟</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>属性选择器</h2>
<div class="cnblogs_code">
<pre>$('[href]')　　<span style="color: #008000;">//</span><span style="color: #008000;">必须带有href属性</span><span style="color: #000000;">
$(</span>'[id=aa]')　<span style="color: #008000;">//</span><span style="color: #008000;">必须有id属性，并且  属性值等于"aa"</span>
$('[id!=aa]')    <span style="color: #008000;">//</span><span style="color: #008000;">其他的都能选择上，唯独id=aa的不选</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$('[class^=c]')　　<span style="color: #008000;">//</span><span style="color: #008000;">必须有class属性，并且  属性值以"c"开头</span><span style="color: #000000;">
$(</span>'[class*=e]') 　　　　<span style="color: #008000;">//</span><span style="color: #008000;">/必须有class属性，并且  属性值含有"e"</span>
$('[class$=d]') 　　<span style="color: #008000;">//</span><span style="color: #008000;">必须有class属性，并且  属性值以"d"结尾</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$('[class$=d] [class*=e] [href]')   <span style="color: #008000;">//</span><span style="color: #008000;">必须多个属性同时满足  才能选择</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">div [class~=bb]　　//div的classname，classname可以有多个类名，并且 bb类名前后 必须有空格</span>

<span style="color: #008000;">//</span><span style="color: #008000;">aside [class|=f]　　　　//aside的classname，必须只有一个类名，并且类名以 f 或 f- 开头的元素</span></pre>
</div>
<p>&nbsp;</p>
<h2>过滤器（child）</h2>
<div class="cnblogs_code">
<pre>$('div&gt;p:first-child')     <span style="color: #008000;">//</span><span style="color: #008000;">div下第一个元素必须是p</span>
<span style="color: #000000;">
$(</span>'div&gt;p:last-child')     <span style="color: #008000;">//</span><span style="color: #008000;">div下最后一个元素必须是p</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$('div&gt;p:nth-child(2)')     <span style="color: #008000;">//</span><span style="color: #008000;">div下第2个元素必须是p</span>
<span style="color: #000000;">
$(</span>'div&gt;p:nth-last-child(2)')     <span style="color: #008000;">//</span><span style="color: #008000;">div下倒数第2个元素必须是p</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$('div&gt;p:only-child')     <span style="color: #008000;">//</span><span style="color: #008000;">div下只有一个元素，且必须是p</span></pre>
</div>
<p>&nbsp;</p>
<h2>过滤器（type）</h2>
<div class="cnblogs_code">
<pre>$('div&gt;p:first-of-type')     <span style="color: #008000;">//</span><span style="color: #008000;">div下可以有多个元素（包括p元素），取第一个p</span>
<span style="color: #000000;">
$(</span>'div&gt;p:last-of-type')     <span style="color: #008000;">//</span><span style="color: #008000;">div下可以有多个元素（包括p元素），取最后一个p</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$('div&gt;p:nth-of-type(2)')     <span style="color: #008000;">//</span><span style="color: #008000;">div下可以有多个元素（包括p元素），取第2个p</span>
<span style="color: #000000;">
$(</span>'div&gt;p:nth-last-of-type(2)')     <span style="color: #008000;">//</span><span style="color: #008000;">div下可以有多个元素（包括p元素），取倒数第2个p</span>

<span style="color: #008000;">//</span><span style="color: #008000;">以上括号参数还可以为odd、even、n，其中n可以2n、3n、2n+1、2n-1等等</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$('div&gt;p:only-of-type')     <span style="color: #008000;">//</span><span style="color: #008000;">div下可以有多个元素，但p只能有一个</span></pre>
</div>
<p>&nbsp;</p>
<h2>表单相关</h2>
<div class="cnblogs_code">
<pre>$(':input')    <span style="color: #008000;">//</span><span style="color: #008000;">选择表单的各种输入元素，如input，textarea，select、button等等。</span>
<span style="color: #000000;">
$(</span>':text')        <span style="color: #008000;">//</span><span style="color: #008000;">选择&lt;input type = 'text' /&gt;</span>
<span style="color: #000000;">
注：$(</span>':typeValue')     <span style="color: #008000;">//</span><span style="color: #008000;">选择&lt;input type = 'typeValue' /&gt;，其中typeValue可以是password  radio  checkbox  image  reset  button  file  等等</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$(':enabled')     <span style="color: #008000;">//</span><span style="color: #008000;">选择表单中的可用元素</span>
<span style="color: #000000;">
$(</span>':disabled')     <span style="color: #008000;">//</span><span style="color: #008000;">选择表单中的禁用元素</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>$(':checked')       <span style="color: #008000;">//</span><span style="color: #008000;">选择表单中被选中的元素，如复选框，单选框，select的option等等</span>
<span style="color: #000000;">
$(</span>':selected')        <span style="color: #008000;">//</span><span style="color: #008000;">选择表单中的select的option，:checked也可以选中，但为了语义化推荐用:selected</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>查找和过滤</h2>
<p>find( expr | object | element )</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> js = $('aside').find('div');    <span style="color: #008000;">//</span><span style="color: #008000;">在aside里面查找所有的div</span></pre>
</div>
<p>&nbsp;</p>
<p>children([expr])</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> di = $('aside').children('div');    <span style="color: #008000;">//</span><span style="color: #008000;">在aside里面找到 子div，不包含孙代</span></pre>
</div>
<p>&nbsp;</p>
<p>parent([expr])</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> pp = di.parent();     <span style="color: #008000;">//</span><span style="color: #008000;">查找di的父代</span></pre>
</div>
<p>&nbsp;</p>
<p>next([expr])</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> a = $('p'<span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> b = a.next();    <span style="color: #008000;">//</span><span style="color: #008000;">查找b后面的一个同辈份的元素</span></pre>
</div>
<p>&nbsp;</p>
<p>prev([expr])</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> a = $('p'<span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> b = a.prev();    <span style="color: #008000;">//</span><span style="color: #008000;">查找b前面的一个同辈份的元素</span></pre>
</div>
<p>&nbsp;</p>
<p>eq(num)</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> li = $('li'<span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> ii = li.eq(3);  <span style="color: #008000;">//</span><span style="color: #008000;">在ii中选择第3个</span>

<span style="color: #0000ff;">var</span> ii = li.eq(-5);  <span style="color: #008000;">//</span><span style="color: #008000;">在ii中选择倒数第5个</span></pre>
</div>
<p>&nbsp;</p>
<p>siblings([expr])</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> v = $('div'<span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> si = v.siblings();   <span style="color: #008000;">//</span><span style="color: #008000;">选择除了v之外的，所有同辈份元素</span></pre>
</div>
<p>&nbsp;</p>
<p>filter( expr | object | element | fn)</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> c = $('li'<span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> c = c.filter('.nb');    <span style="color: #008000;">//</span><span style="color: #008000;">在c中选择带有 nb类名 的元素</span>

<span style="color: #008000;">//</span><span style="color: #008000;">若参数为function(index){ console.log(index);  //index表示c里面元素的索引值 }</span></pre>
</div>
<p>&nbsp;</p>
<p>注：num表示数字，[]里面表示可选，ecpr表示字符串，object表示现有的jquery对象(用jquery选择的对象)，element表示Dom元素名，fn表示函数(用来作为测试元素的集合)</p>
