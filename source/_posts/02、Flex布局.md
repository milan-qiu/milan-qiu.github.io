---
title: "02、Flex布局"
date: "2020-04-15 13:17:00"
tags:
categories:
description: >-
  Flex布局 //Flex 是 Flex Box 的缩写，意为“灵活的盒子”或“弹性的盒子”，所以flex布局一般称为弹性布局。 flex容器：所有含有 display:flex | inline-flex; 的容器都是flex容器。 flex项目：flex容器的所有子元素都是flex项目。（不包括
---

<h2>Flex布局</h2>
<p>//Flex 是 Flex Box 的缩写，意为&ldquo;灵活的盒子&rdquo;或&ldquo;弹性的盒子&rdquo;，所以flex布局一般称为弹性布局。</p>
<p>flex容器：所有含有 display:flex | inline-flex; 的容器都是flex容器。</p>
<p>flex项目：flex容器的所有子元素都是flex项目。（不包括孙元素）</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200414103628379-972089365.png" alt="" width="549" height="325" /></p>
<p>容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做<code>main start</code>，结束位置叫做<code>main end</code>；交叉轴的开始位置叫做<code>cross start</code>，结束位置叫做<code>cross end</code>。</p>
<p>项目默认沿主轴排列。单个项目占据的主轴空间叫做<code>main size</code>，占据的交叉轴空间叫做<code>cross size</code>。</p>
<h3>display属性</h3>
<p>display:flex;</p>
<p>沿主轴方向，作为弹性伸缩盒显示，有固定宽度。</p>
<p>display:inline-flex;</p>
<p>沿主轴方向，作为弹性伸缩盒显示，宽度由内容撑开。</p>
<p>//类似display:block与display:inline-block</p>
<p>&nbsp;</p>
<h2>容器属性&nbsp;</h2>
<h3>flex-direction属性</h3>
<p>//<strong>决定主轴的排列方向</strong>，默认 flex-direction:row ，起点在左边</p>
<p>row-reverse</p>
<p>主轴为水平方向，起点在右边</p>
<p>column</p>
<p>主轴为垂直方向，从上往下排</p>
<p>column-reverse</p>
<p>主轴为垂直方向，从下往上排</p>
<p>&nbsp;</p>
<h3>flex-wrap属性</h3>
<p>//<strong>决定是否换行和怎样换行</strong>，默认flex-wrap:nowrap; 默认不会换行，所有东西都压缩到一行显示。</p>
<p>wrap</p>
<p>自动换行，不会压缩，第一行在上面，依次往下换行</p>
<p>wrap-reverse</p>
<p>自动换行，不会压缩，第一行在最下面，依次往上换行。</p>
<p>&nbsp;</p>
<h3>flex-flow属性</h3>
<p>//是<strong>flow-direction&nbsp; 与&nbsp; flow-wrap的组合写法</strong>，默认flex-flow:row&nbsp; nowrap;</p>
<p>&nbsp;</p>
<h3>justify-content属性</h3>
<p>//<strong>决定项目主轴的对齐方式</strong>，默认 justify-content:flex-start&nbsp; 默认左对齐</p>
<p>flex-end：项目右对齐</p>
<p>flex-center：项目居中对齐</p>
<p>space-between：两端对齐，项目之间的间隔相等</p>
<p>space-around：每个项目两侧的间隔相等，所以，项目之间的间隔比项目与边框的间隔大一倍。&nbsp;</p>
<p>&nbsp;</p>
<h3>align-items属性</h3>
<p>&nbsp;//决定项目在交叉轴上的对齐方式，默认stretch，若项目未设置高度，或设置auto，将占满整个容器高度</p>
<p>flex-start：交叉轴的<strong>起点对齐</strong></p>
<p>flex-end：交叉轴的<strong>终点对齐</strong></p>
<p>center：交叉轴的<strong>中点对齐</strong></p>
<p>baseline：项目<strong>第一行文字的基线对齐</strong></p>
<p>&nbsp;</p>
<h3>align-content属性&nbsp;</h3>
<p>//定义了多根轴线（多行）在交叉轴上的对齐方式；若项目只有一根轴线（一行），该属性不起作用。</p>
<p>stretch（默认值）：项目若不定义高度，或定义为auto。轴线占满整个高度</p>
<p>flex-start：交叉轴的起点对齐</p>
<p>flex-end：交叉轴的终点对齐</p>
<p>flex-center：交叉轴的中点对齐</p>
<p>space-between：交叉轴两端对齐，轴线之间的间隔平均分布</p>
<p>space-around：每根轴线两侧的间隔都相等，所以，轴线之间的间隔比轴线与边框的间隔大一倍。</p>
<p>&nbsp;</p>
<h2>项目的属性</h2>
<h3>order属性</h3>
<p>//定义项目的排列顺序，数值越小排列越靠前，默认为0</p>
<p>order:-1;</p>
<p>&nbsp;</p>
<h3>flex-grow属性</h3>
<p>//瓜分剩余空间的属性</p>
<p>//定义项目的放大属性，默认为0，即如果存在剩余空间也不放大。</p>
<p>//如果所有的项目flex-grow属性都为1，则它们将瓜分剩余空间（如果有的画）</p>
<p>//如果一个项目的flex-grow属性为2，其他都为1，则前者瓜分的剩余空间将比其他项目多一倍</p>
<p>flex-grow:2;</p>
<p>&nbsp;</p>
<h3>flex-shrink属性</h3>
<p>//定义项目的缩小比例，<strong>默认为1</strong>，即若空间不足，该项目将缩小。负值对该属性无效</p>
<p>//如果项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。</p>
<p>//如果一个项目flex-shrink属性为0，其他项目都为1，空间不足时，前者不缩小，后者都按比例缩小</p>
<p>flex-shrink:0;&nbsp;</p>
<p>&nbsp;</p>
<h3>flex-basis属性（*）</h3>
<p>//定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为<code>auto</code>，即项目的本来大小。</p>
<p>//它可以设为跟<code>width</code>或<code>height</code>属性一样的值（比如350px），则项目将占据固定空间。</p>
<p>flex-basis:300px;</p>
<p>&nbsp;</p>
<h3>flex属性</h3>
<p>//是flex-grow、flex-shrink、flex-basis的组合写法。默认值 flex:0 1 auto</p>
<p>//1参数必选(flex-grow)，23参数可选(flex-shrink、flex-basis)&nbsp;</p>
<p>flex:1;&nbsp; //瓜分剩余空间，相当于flex-grow</p>
<p>&nbsp;</p>
<h3>align-self属性</h3>
<p>//允许单个项目与其他项目不一样的对齐方式，可覆盖align-items属性。<strong>默认值auto</strong>，表示继承父元素的align-items属性，若没有父元素，则等同于stretch</p>
<p>flex-start：起点对齐</p>
<p>flex-end：终点对齐</p>
<p>flex-center：中点对齐</p>
<p>baseline：基线对齐</p>
<p>stretch：项目若不定义高度，或定义为auto。轴线占满整个高度</p>
