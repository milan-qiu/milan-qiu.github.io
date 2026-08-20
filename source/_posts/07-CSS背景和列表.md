---
title: "07-CSS背景和列表"
date: "2020-01-18 12:13:00"
tags:
categories:
description: >-
  vertical-align（垂直对齐） baseline：默认。元素放置在父元素的基线上。super：垂直对齐文本的上标sub：垂直对齐文本的下标。 text-top：把元素的顶端与父元素字体的顶端对齐text-bottom：把元素的底端与父元素字体的底端对齐。 top：把元素的顶端与行中最高元素
---

<p><span style="font-family: 幼圆; font-size: 16px;"><strong>vertical-align（垂直对齐）</strong></span></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<p>baseline：默认。元素放置在父元素的基线上。<br />super：垂直对齐文本的上标<br />sub：垂直对齐文本的下标。</p>
<p>text-top：把元素的顶端与父元素字体的顶端对齐<br />text-bottom：把元素的底端与父元素字体的底端对齐。</p>
<p><br />top：把元素的顶端与行中最高元素的顶端对齐<br />middle：把此元素放置在父元素的中部。<br />bottom：把元素的底端与行中最低的元素的顶端对齐。</p>
<p>length：长度单位   <br />%：使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。<br />inherit：规定应该从父元素继承 vertical-align 属性的值。</p>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>background-repeat（背景重复）</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">repeat：重复

no-repeat：不重复

repeat-x：水平方向重复

repeat-y：垂直方向重复</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>background-attachment（背景 是否随页面内容 滚动而滚动）</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">scroll：背景随页面内容滚动

fixed：背景不会随页面内容滚动，fixed是相对于整个网页来说的</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>background-possision（设置背景图像的起始位置）</strong></span></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">left top
left center
left bottom
right top
right center
right bottom
center top
center center
center bottom    如果仅指定一个关键字，其他值将会是"center"<br />
x% y%    第一个值是水平位置，第二个值是垂直。左上角是0％0％。右下角是100％100％。如果仅指定了一个值，其他值将是50％。 。默认值为：0％0％
xpos ypos    第一个值是水平位置，第二个值是垂直。左上角是0。单位可以是像素（0px0px）或任何其他 CSS单位。如果仅指定了一个值，其他值将是50％。你可以混合使用％和positions
inherit    指定background-position属性设置应该从父元素继承</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>background（缩写）</strong><br /></span></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>background:[background-color] [background-image] [background-repeat] [background-attachment] [background-position]<br />//各值之间用空格分割，不分先后顺序</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>list-style-type（有序、无序列表样式）</strong></span></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">有序列表
none：无标记
decimal：从1开始的整数
lower-roman：小写罗马数字
lower-alpha：小写英文字母
upper-alpha：大写英文字母

无序列表
none：无标记
disc：实心圆点
circle：空心圆点
square：实心方块</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">把列表的序号改成小图标</span></strong></p>
<div class="cnblogs_code">
<pre>list-style-image : url() ;</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>list-style-position（文本 是否环绕 列表图标）</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">outside：不环绕列表图标（默认）

inside：环绕列表图标</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>list-style（缩写）</strong><br /></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">list-style : [list-style-type] [list-style-position] [list-style-image]
//值之间用空格分割，顺序不固定，list-style-image会覆盖list-style-type</span></pre>
</div>
