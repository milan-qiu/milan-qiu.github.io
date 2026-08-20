---
title: "01-HTML5标签变化"
date: "2020-01-18 15:29:00"
updated: "2020-04-11 22:24:00"
tags:
categories:
description: >-
  结构标签（有意义的div） <header>标记定义一个页面或一个区域的头部</header> <nav>标记定义导航链接</nav> <section>标记定义一个区域</section> <article>标记定义一篇文章</article> <aside>标记定义页面内容部分的侧边栏</asi
---

<p><strong><span style="font-family: 幼圆; font-size: 14pt;">结构标签（有意义的div）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">header</span><span style="color: #0000ff;">&gt;</span>标记定义一个页面或一个区域的头部<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">header</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">nav</span><span style="color: #0000ff;">&gt;</span>标记定义导航链接<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">nav</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">section</span><span style="color: #0000ff;">&gt;</span>标记定义一个区域<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">section</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">article</span><span style="color: #0000ff;">&gt;</span>标记定义一篇文章<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">article</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">aside</span><span style="color: #0000ff;">&gt;</span>标记定义页面内容部分的侧边栏<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">aside</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">hgroup</span><span style="color: #0000ff;">&gt;</span>标记定义文件中一个区块的相关信息<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">hgroup</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">figure</span><span style="color: #0000ff;">&gt;</span>标记定义一组媒体内容以及它们的标题<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">figure</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">figcaption</span><span style="color: #0000ff;">&gt;</span>标记定义figure元素的标题<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">figcaption</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dialog</span><span style="color: #0000ff;">&gt;</span>标记定义一个对话框（类似微信会话框）<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dialog</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">footer</span><span style="color: #0000ff;">&gt;</span>标记定义一个页面或一个区域的底部<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">footer</span><span style="color: #0000ff;">&gt;<br /><br /></span></pre>
<p>//header/section/aside/article/footer 标签不要嵌套使用</p>
<p>//header/section/footer 大于 aside/article/figure/hgroup/nav 大于 div/figcaption</p>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>新增加的多媒体标签</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">video</span><span style="color: #0000ff;">&gt;</span>标记定义一个视频<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">video</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">audio</span><span style="color: #0000ff;">&gt;</span>标记定义音频内容<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">audio</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">canvas</span><span style="color: #0000ff;">&gt;</span>标记定义图片<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">canvas</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">标记定义媒体资源
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">embed</span><span style="color: #0000ff;">&gt;</span>标记定义外部的可交互的内容或插件，比如flash<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">embed</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong><span style="font-size: 14pt;">音频标签</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">audio</span><span style="color: #0000ff;">&gt;</span>不支持audio标签才会显示这段文字<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">audio</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">1、src属性：直接引入音频</span><br /><span style="font-family: 幼圆; font-size: 16px;">2、autoplay="autoplay"，音频自动播放</span><br /><span style="font-family: 幼圆; font-size: 16px;">3、loop="-1&Prime;，音频无限循环</span><br /><span style="font-family: 幼圆; font-size: 16px;">4、controls = "controls"，使用浏览器的音频播放</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">如果audio标签里面有多个音频文件，可以用：</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">audio</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="xxx.mp3&Prime; type="</span><span style="color: #ff0000;">audio/mpeg"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//音频文件转码用：type="audio/mpeg"（audio里面的mp3文件）
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="aaa.mp3&Prime; type="</span><span style="color: #ff0000;">audio/mpeg"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">audio</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong><span style="font-size: 14pt;">视频标签</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">video </span><span style="color: #ff0000;">width</span><span style="color: #0000ff;">="1024px"</span><span style="color: #ff0000;"> height</span><span style="color: #0000ff;">="800px"</span><span style="color: #0000ff;">&gt;</span>不支持video标签才会显示这段文字<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">video</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">1、src属性：直接引入音频</span><br /><span style="font-family: 幼圆; font-size: 16px;">2、autoplay="autoplay"，音频自动播放</span><br /><span style="font-family: 幼圆; font-size: 16px;">3、loop="-1&Prime;，音频无限循环</span><br /><span style="font-family: 幼圆; font-size: 16px;">4、controls = "controls"，使用浏览器的音频播放</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">如果video标签里面有多个音频文件，可以用：</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">video</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="xxx.mp4&Prime; type="</span><span style="color: #ff0000;">video/mp4&Prime;</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">//视频文件转码用：type="video/mp4&Prime;（video里面的mp4文件）
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="aaa.mp4&Prime; type="</span><span style="color: #ff0000;">video/mp4"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">video</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>外部的可交互的内容或插件 使用</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">embed </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="xxx.swf"</span><span style="color: #ff0000;"> width</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> height</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">embed</span><span style="color: #0000ff;">&gt;　　</span>//embed一般用来引用flash文件</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>新增加的web应用标签</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meter</span><span style="color: #0000ff;">&gt;</span>状态标签（实时状态显示：气压、气温）<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">meter</span><span style="color: #0000ff;">&gt;<br /></span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">progress </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> max</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>状态标签（任务过程：安装、加载）</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">meter //实时显示气压、气温</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meter </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="220&Prime;      min="</span><span style="color: #ff0000;">20&Prime;   max</span><span style="color: #0000ff;">="380&Prime;       low="</span><span style="color: #ff0000;">200&Prime;           high</span><span style="color: #0000ff;">="240&Prime;         optimum="</span><span style="color: #ff0000;">220&Prime;</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">meter</span><span style="color: #0000ff;">&gt;</span>
value：自定义的值<br />min：最小<br />max：最大<br />low：安全最低<br />high：安全最高<br />optimum：最佳<br /><br /><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meter </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="0.75&Prime;&gt;&lt;/meter&gt; //直接到75%的位置</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">progress //任务加载过程</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">progress </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="30&Prime; max="</span><span style="color: #ff0000;">100&Prime;</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//进度条会在30%的位置

</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">progress </span><span style="color: #ff0000;">max</span><span style="color: #0000ff;">="100&Prime;&gt;　　//进度条会来回转动</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">新增加的列表标签</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">datalist</span><span style="color: #0000ff;">&gt;</span>为input标记定义一个下拉列表，配合option<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">datalist</span><span style="color: #0000ff;">&gt;<br /></span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">details</span><span style="color: #0000ff;">&gt;</span>标记定义一个元素的详细内容，配合summary<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">details</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">datalist&nbsp; &nbsp;//选择列表</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">placeholder</span><span style="color: #0000ff;">="请选择xxx"</span><span style="color: #ff0000;"> list</span><span style="color: #0000ff;">="qml"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">datalist </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="qml"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="aa"</span><span style="color: #0000ff;">&gt;</span>aa<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="bb"</span><span style="color: #0000ff;">&gt;</span>bb<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="cc"</span><span style="color: #0000ff;">&gt;</span>cc<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="dd"</span><span style="color: #0000ff;">&gt;</span>dd<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="ee"</span><span style="color: #0000ff;">&gt;</span>ee<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">datalist</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">details //详细展示</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">details </span><span style="color: #ff0000;">open</span><span style="color: #0000ff;">="open"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//open表示默认是打开
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">summary</span><span style="color: #0000ff;">&gt;</span>自定义的详细信息<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">summary</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>详细信息详细信息详细信息详细信息详细信息详细信息<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">details</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>新增加的其他标签</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ruby</span><span style="color: #0000ff;">&gt;</span>标记定义注释或音标<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ruby</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">rt</span><span style="color: #0000ff;">&gt;</span>标记定义对ruby的注释内容文本<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">rt</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">rp</span><span style="color: #0000ff;">&gt;</span>告诉那些不支持ruby元素的浏览器，如何显示<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">rp</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">mark</span><span style="color: #0000ff;">&gt;</span>标记定义有标记的文本（黄色选中状态）<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">mark</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">output</span><span style="color: #0000ff;">&gt;</span>标记定义一些输出类型，计算表单结果，配合oninput<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">output</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">ruby注释标签</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>这个"<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ruby</span><span style="color: #0000ff;">&gt;</span>    丘 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">rt</span><span style="color: #0000ff;">&gt;</span>qiu<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">rt</span><span style="color: #0000ff;">&gt;</span>    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ruby</span><span style="color: #0000ff;">&gt;</span>"字怎么念<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">

//对于不支持的浏览器可以加rp：
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>这个"<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ruby</span><span style="color: #0000ff;">&gt;</span>    丘<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">rp</span><span style="color: #0000ff;">&gt;</span>(<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">rp</span><span style="color: #0000ff;">&gt;</span>    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">rt</span><span style="color: #0000ff;">&gt;</span>qiu<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">rt</span><span style="color: #0000ff;">&gt;</span>    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">rp</span><span style="color: #0000ff;">&gt;</span>）<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">rp</span><span style="color: #0000ff;">&gt;</span>    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ruby</span><span style="color: #0000ff;">&gt;</span>"字怎么念<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">mark标记文本</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span> 有两个字会变   <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">mark</span><span style="color: #0000ff;">&gt;</span>黄色<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">mark</span><span style="color: #0000ff;">&gt;</span>   <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">output做简单计算器</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form </span><span style="color: #ff0000;">oninput</span><span style="color: #0000ff;">="totalPrice.value = parseInt(price.value) * parseInt(number.value)"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="number"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="price"</span><span style="color: #ff0000;"> placeholder</span><span style="color: #0000ff;">="输入一个数"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
*</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="number"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="number"</span><span style="color: #ff0000;"> placeholder</span><span style="color: #0000ff;">="输入另外一个数"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
=</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">output </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="totalPrice"</span><span style="color: #ff0000;"> for</span><span style="color: #0000ff;">="price number"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">output</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;">重定义标签：显示不变,只是表达的含义进行了重新定义的标签</span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">b</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">b</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">代表内联文本,通常是粗体,没有传递表示重要的意思
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">i</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">i</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">代表内联文本,通常是斜体,没有传递表示重要的意思

</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dd</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">dd</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">可以同 details 与 figure 一同使用,定义包含文本,dialog也可用
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dt</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">dt</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">可以同 details 与 figure 一同使用,汇总细节, dialog也可用

</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">hr</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">不仅表示水平线,还表示主题结束,显示效果相同
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">menu</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">menu</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">重新定义用户界面的菜单,配合 command或者 menuitem使用

</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">smal</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">smal</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">表示小字体,例如打印注释或者法律条款
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">strong</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">strong</span><span style="color: #0000ff;">&gt;</span>表示重要性而不是强调符号</pre>
</div>
