---
title: "01、jQuery入门"
date: "2020-03-14 12:06:00"
tags:
categories:
description: >-
  jQuery是什么？ jQuery是一个快速、小巧且功能丰富的JavaScript库。 jQuery下载及引入 下载地址：www.jquery.com //根据需求可下载压缩版 或者 未压缩版。 引入：在head里面 或者 body里面，<script type="text/javascript"
---

<h2>jQuery是什么？</h2>
<p>jQuery是一个快速、小巧且功能丰富的JavaScript库。</p>
<p>&nbsp;</p>
<h2>jQuery下载及引入</h2>
<p>下载地址：www.jquery.com&nbsp; &nbsp; //根据需求可下载压缩版&nbsp; 或者&nbsp; 未压缩版。</p>
<p>引入：在head里面&nbsp; 或者&nbsp; body里面，&lt;script type="text/javascript" src="js/jquery-3.4.1.min.js"&gt;&lt;/script&gt;</p>
<p>&nbsp;</p>
<p>注：$===jQuery&nbsp; &nbsp; //当$被占用的时候，可以用jQuery代替</p>
<p>&nbsp;</p>
<h2>html加载完毕后，执行js</h2>
<p>原生写法：</p>
<div class="cnblogs_code">
<pre>window.onload = <span style="color: #0000ff;">function</span>(){   };</pre>
</div>
<p>&nbsp;</p>
<p>jQuery写法：</p>
<div class="cnblogs_code">
<pre>$(document).ready.(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){   });

$().ready.(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(){   });

$(</span><span style="color: #0000ff;">function</span>(){   });</pre>
</div>
<p>&nbsp;</p>
<h2>css、html、text方法</h2>
<p>//css</p>
<div class="cnblogs_code">
<pre>$('p').css({      <span style="color: #008000;">//</span><span style="color: #008000;">获取p标签，更改p标签css样式</span>

"background-color":"lightgreen"<span style="color: #000000;">,

</span>"color":"white"<span style="color: #000000;">
});</span></pre>
</div>
<p>&nbsp;</p>
<p>//html</p>
<div class="cnblogs_code">
<pre>$('div').html(      <span style="color: #008000;">//</span><span style="color: #008000;">获取div标签，替换div原来的所有内容</span>

'&lt;p&gt;你好&lt;/p&gt;'<span style="color: #000000;">
);</span></pre>
</div>
<p>&nbsp;</p>
<p>//text</p>
<div class="cnblogs_code">
<pre>$('p').text(       <span style="color: #008000;">//</span><span style="color: #008000;">获取p标签，替换p原来的文本</span>

'你好'<span style="color: #000000;">
);</span></pre>
</div>
<p>&nbsp;</p>
