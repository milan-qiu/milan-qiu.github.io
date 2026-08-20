---
title: "09-CSS定位（position）"
date: "2020-01-18 14:29:00"
updated: "2020-01-18 14:32:00"
tags:
categories:
description: >-
  静态定位：使元素定位于常规流中 position: static; 1、忽略top,bottom,left,right,z-index。2、两个相邻元素如果设置了外边距，最终外边距 = 两者外边距最大的。3、具有 固定的width和height值的元素，如果左右外边距设置成auto，左右外边距会自动
---

<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>静态定位：使元素定位于常规流中</strong></span></p>
<div class="cnblogs_code">
<pre>position: static;</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">1、忽略top,bottom,left,right,z-index。</span><br /><span style="font-family: 幼圆; font-size: 16px;">2、两个相邻元素如果设置了外边距，最终外边距 = 两者外边距最大的。</span><br /><span style="font-family: 幼圆; font-size: 16px;">3、具有 固定的width和height值的元素，如果左右外边距设置成auto，左右外边距会自动扩大占满剩余宽度。造成的效果就是水平居中。</span></p>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>相对定位：使元素成为 containing-block（可定位的祖先元素）</strong></span></p>
<div class="cnblogs_code">
<pre>position: relative;</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">1、可以使用top,bottom,left,right,z-index 进行相对定位。</span><br /><span style="font-family: 幼圆; font-size: 16px;">2、相对定位的元素不会离开常规流。</span><br /><span style="font-family: 幼圆; font-size: 16px;">3、任何元素都可以设置relative，它的绝对定位的后代 都可以相对于它 进行绝对定位</span><br /><span style="font-family: 幼圆; font-size: 16px;">4、可以使浮动元素发生偏移，并控制它们的堆叠顺序。</span></p>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>绝对定位：使元素脱离常规流</strong></span></p>
<div class="cnblogs_code">
<pre>position: absolute;</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">1、脱离常规流</span><br /><span style="font-family: 幼圆; font-size: 16px;">2、设置尺寸要注意，百分比比的是最近定位的祖先元素</span><br /><span style="font-family: 幼圆; font-size: 16px;">3、top,bottom,left,right 设置为0，它将对齐到最近定位祖先元素的各边。</span><br /><span style="font-family: 幼圆; font-size: 16px;">4、top,bottom,left,right 设置为auto，它将会打回原形</span><br /><span style="font-family: 幼圆; font-size: 16px;">5、如果没有 最近定位祖先元素，就会 把body当 最近定位祖先元素</span><br /><span style="font-family: 幼圆; font-size: 16px;">6、z-index可以控制堆叠顺序（最高999999）</span></p>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>固定定位：</strong></span></p>
<div class="cnblogs_code">
<pre>position: fixed;</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">1、相对于整个屏幕做绝对定位</span><br /><span style="font-family: 幼圆; font-size: 16px;">2、固定定位不会随着视口滚动而滚动</span><br /><span style="font-family: 幼圆; font-size: 16px;">3、继承absolute的特点</span></p>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 14pt;"><strong>粘性定位： relative + fixed 的完美结合，制造出吸附效果</strong></span></p>
<div class="cnblogs_code">
<pre>position: sticky;</pre>
</div>
<p><span style="font-family: 幼圆; font-size: 16px;">1、如果产生偏移 原位置还是会在常规流中（相对定位的特性）</span><br /><span style="font-family: 幼圆; font-size: 16px;">2、如果它的 最近祖先元素 有滚动 那么它的偏移标尺 就是最近祖先元素</span><br /><span style="font-family: 幼圆; font-size: 16px;">3、如果它的 最近祖先元素 没有滚动 那么它的偏移标尺 是视口</span><br /><span style="font-family: 幼圆; font-size: 16px;">4、上下左右偏移规则都一样</span></p>
