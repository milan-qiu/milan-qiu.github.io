---
title: "02-HTML5属性变化"
date: "2020-01-18 16:59:00"
updated: "2020-04-11 22:30:00"
tags:
categories:
description: >-
  input新增属性 datepickers <input type="email" name="">//手机端会有@xxx.com输入提示 <input type="url" name=""> //手机端会有.com输入提示 <input type="tel" name="">//安卓手机端会出现简
---

<h1><span style="font-family: 幼圆; font-size: 14pt;"><strong>input新增属性</strong></span></h1>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>datepickers</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="email" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">//手机端会有<strong>@xxx.com输入提示</strong><br />
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="url" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;"> //手机端会有<strong>.com输入提示</strong><br />
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="tel" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">//安卓手机端会出现简洁的九宫格<strong>数字</strong>输入<br />
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="number" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">//手机端会出现简洁的九宫格数字输入（只能输入<strong>数字或者简单的运算符号</strong>）<br />
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="date" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;"> //手机端会出现 <strong>年 月 日</strong> 的选择<br />
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="month" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">//手机端会出现 <strong>年 月</strong>的选择<br />
</span><span style="text-decoration: line-through;"><span style="color: #0000ff; text-decoration: line-through;">&lt;</span><span style="color: #800000; text-decoration: line-through;">input </span><span style="color: #ff0000; text-decoration: line-through;">type</span><span style="color: #0000ff; text-decoration: line-through;">="week" </span><span style="color: #ff0000; text-decoration: line-through;">name</span><span style="color: #0000ff; text-decoration: line-through;">=""</span><span style="color: #0000ff; text-decoration: line-through;">&gt;</span></span><span style="color: #000000;"><span style="text-decoration: line-through;">//手机端会出现 年 周 的选择，iphone已不支持</span><br />
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="time" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">//手机端会出现<strong> 时 分</strong> 的选择<br />
</span><span style="text-decoration: line-through;"><span style="color: #0000ff; text-decoration: line-through;">&lt;</span><span style="color: #800000; text-decoration: line-through;">input </span><span style="color: #ff0000; text-decoration: line-through;">type</span><span style="color: #0000ff; text-decoration: line-through;">="datetime" </span><span style="color: #ff0000; text-decoration: line-through;">name</span><span style="color: #0000ff; text-decoration: line-through;">=""</span><span style="color: #0000ff; text-decoration: line-through;">&gt;</span><span style="color: #000000; text-decoration: line-through;">////手机端会出现 年 月 日 时 分 的选择，（很多手机已不兼容，pc端也如此）<br />
</span></span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="datetime-local" </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>//手机端会出现 月 日 周 时 分 的选择</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">range摇杆选择</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="range"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> min</span><span style="color: #0000ff;">="1&Prime; max="</span><span style="color: #ff0000;">10&Prime;</span><span style="color: #0000ff;">&gt;　　</span>//摇杆选择，默认最大100</pre>
</div>
<p>&nbsp;</p>
<p><strong>search搜索框</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="search"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;　　</span>//文本输入框后面多了一个叉</pre>
</div>
<p>&nbsp;</p>
<p><strong>color颜色选择框</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="color"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;　　</span>//点击按钮会出现颜色选择器</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>表单新增属性</strong></span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>autocomplete属性（表单自动填充）</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form </span><span style="color: #ff0000;">action</span><span style="color: #0000ff;">="xxx.php"</span><span style="color: #ff0000;"> autocomplete</span><span style="color: #0000ff;">="on"</span><span style="color: #0000ff;">&gt;　　//表单根据历史记录，自动填充</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="number"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> autocomplete</span><span style="color: #0000ff;">="off"</span><span style="color: #0000ff;">&gt;　　//该输入框取消自动填充</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="submit"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;<br /><br />//autocomplete适用于input的：text,search,url,telephone,email,password,datepickers,range,color</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">&nbsp;autofocus属性（页面加载后，该输入框自动获得焦点）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form </span><span style="color: #ff0000;">action</span><span style="color: #0000ff;">="xxx.php"</span> <span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> autofocus</span><span style="color: #0000ff;">="autofocus"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//页面加载时光标自动进入输入框
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="number"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span> <span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="submit"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;<br /><br />//autofocus适用于所有input</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">&nbsp;multiple属性（按ctrl可以选择多个值）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form </span><span style="color: #ff0000;">action</span><span style="color: #0000ff;">="xxx.php"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="file"</span><span style="color: #ff0000;"> multiple</span><span style="color: #0000ff;">="multiple"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//按住ctrl键可以选择多个文件
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="email"</span><span style="color: #ff0000;"> multiple</span><span style="color: #0000ff;">="multiple"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//一个邮箱结束后 用逗号隔开 还可以输入另外一个邮箱
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="submit"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">placeholder属性（输入框提示信息）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="search"</span><span style="color: #ff0000;"> placeholder</span><span style="color: #0000ff;">="输入框提示信息"</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">required属性（输入框不按照规则输入，无法提交）&nbsp;</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> required</span><span style="color: #0000ff;">="required"</span><span style="color: #0000ff;">&gt;　　</span><span style="color: #000000;">//对输入框进行判断，必须有内容
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="email"</span><span style="color: #ff0000;"> required</span><span style="color: #0000ff;">="required"</span><span style="color: #0000ff;">&gt;　　</span>//对邮箱判断，必须符合邮箱规则<br /><br />适用于input的：text,search,url,telephone,email,password,date pickers,number,checkbox,radio,file</pre>
</div>
<p>&nbsp;</p>
<h2><span style="font-family: 幼圆; font-size: 14pt;"><strong>链接属性</strong></span></h2>
<h3><span style="font-family: 幼圆; font-size: 16px;"><strong>sizes（为了在不同屏幕上，网站图标都保持清晰）</strong></span></h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="icon"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="image/png"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="xxx.png"</span><span style="color: #ff0000;"> sizes</span><span style="color: #0000ff;">="16*16"</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<h3><strong><span style="font-size: 16px; font-family: 幼圆;">target属性（控制是否打开新窗口）</span></strong></h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">base </span><span style="color: #ff0000;">href</span><span style="color: #0000ff;">="http://localhost/"</span><span style="color: #ff0000;"> target</span><span style="color: #0000ff;">="_blank"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">

//base写在head里面
//base里面的href表示，页面每一个超链接前面都添加localhost
//base里面的target表示，页面每一个超链接都打开新窗口</span></pre>
</div>
<p>&nbsp;</p>
<h3><strong><span style="font-size: 16px; font-family: 幼圆;">a标签的media属性（表示该链接要对某种设备进行支持，如handheld/tv）</span></strong></h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">a </span><span style="color: #ff0000;">href</span><span style="color: #0000ff;">="xxx.com"</span><span style="color: #ff0000;"> media</span><span style="color: #0000ff;">="handheld"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span>    //表示该链接要对手持设备进行支持</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 16px; font-family: 幼圆;">a标签的hreflang属性（表示该链接到的页面，是xx的编码方式）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">a </span><span style="color: #ff0000;">href</span><span style="color: #0000ff;">="xxx.com"</span><span style="color: #ff0000;"> hreflang</span><span style="color: #0000ff;">="hk"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 16px; font-family: 幼圆;">a标签的rel属性（表示该链接的类型，是什么类型）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">a </span><span style="color: #ff0000;">href</span><span style="color: #0000ff;">="xxx.com"</span><span style="color: #ff0000;"> rel</span><span style="color: #0000ff;">="external"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span>  //表示链接的引用是个外部链接</pre>
</div>
<p>&nbsp;</p>
<p><span style="text-decoration: line-through;"><strong><span style="font-family: 幼圆; font-size: 16px;">defer 属性（script加载完不执行，等待页面加载完之后再执行</span><span style="font-family: 幼圆; font-size: 16px;">）</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="text-decoration: line-through;"><span style="color: #0000ff; text-decoration: line-through;">&lt;</span><span style="color: #800000; text-decoration: line-through;">script </span><span style="color: #ff0000; text-decoration: line-through;">defer type</span><span style="color: #0000ff; text-decoration: line-through;">="text/javascript"</span><span style="color: #ff0000; text-decoration: line-through;"> src</span><span style="color: #0000ff; text-decoration: line-through;">="er.js"</span><span style="color: #0000ff; text-decoration: line-through;">&gt;&lt;/</span><span style="color: #800000; text-decoration: line-through;">script</span><span style="color: #0000ff; text-decoration: line-through;">&gt;　　</span>//加载完整个网页再执行（目前暂不支持高版本浏览器）</span><br /><br /><span style="text-decoration: line-through;">//只能用于src，该属性都会使网页加载<strong>变</strong>成&nbsp;&nbsp;双线程<strong>，</strong>速度大大提高。</span><br /><span style="text-decoration: line-through;">//<strong>只有 Internet Explorer 支持 defer 属性</strong>。</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">async 属性（加载后直接执行）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">async type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="yi.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>//直接加载执行，异步执行<br /><br />//只能用于src，该属性都会使<strong>网页</strong>加载<strong>变成</strong>&nbsp;&nbsp;<strong>双线程，</strong>速度大大提高。</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">&nbsp;</span></p>
<p><span style="font-size: 14pt;"><strong><span style="font-family: 幼圆;">start属性 和 reversed属性 （有序列表）</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ol </span><span style="color: #ff0000;">start</span><span style="color: #0000ff;">="10"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">        //从第10条开始显示
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>1<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>2<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>3<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
    ......
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ol</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ol </span><span style="color: #ff0000;">reversed</span><span style="color: #0000ff;">="reversed"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">    //列表倒序显示
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>1<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>2<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>3<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
    ......
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ol</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>mainifest="cache.mainifest"</strong> （</span><span style="font-family: 幼圆; font-size: 16px;"><strong>电脑离线的时候加载网页）</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html </span><span style="color: #ff0000;">mainifest</span><span style="color: #0000ff;">="cache.mainifest"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">

//默认保存index.html  ,  index.css  ,  index.js</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>scoped属性 （<span style="font-family: 幼圆;">页面任何一个地方都可以写style）</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">style </span><span style="color: #ff0000;">scoped</span><span style="color: #0000ff;">&gt;</span><span style="background-color: #f5f5f5; color: #800000;">  样式可以写进body的任何一个地方，不仅仅是head  </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">style</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
