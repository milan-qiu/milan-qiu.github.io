---
title: "02、CSS基础"
date: "2020-05-09 17:03:00"
tags:
categories:
description: >-
  link标签和import标签的区别 1、link属于html标签，而@import是css提供的 2、页面被加载时，link会同时被加载，而@import引用的css会等到页面加载结束后加载。 3、link是html标签，因此没有兼容性，而@import只有IE5以上才能识别。 4、link方式样
---

<h3>link标签和import标签的区别</h3>
<div>1、link属于html标签，而@import是css提供的</div>
<p>2、页面被加载时，link会同时被加载，而@import引用的css会等到页面加载结束后加载。</p>
<p>3、link是html标签，因此没有兼容性，而@import只有IE5以上才能识别。</p>
<p>4、link方式样式的权重高于@import的。</p>
<p>&nbsp;</p>
<h3>CSS盒模型</h3>
<p>就是用来装页面上的元素的矩形区域。CSS中的盒子模型包括<strong>IE盒模型</strong>和标准的<strong>W3C盒模型</strong>。</p>
<p>IE盒模型只在IE5及以前版本使用，IE6及以后都是使用W3C盒模型。</p>
<p>&nbsp;</p>
<p>一、可以手动设置盒模型（宽高的计算方式）</p>
<p>box-sizing : border-box | padding-box | content-box&nbsp; | inherit&nbsp; &nbsp; &nbsp; &nbsp;//padding-box是火狐私有属性。inherit继承父元素的box-sizing&nbsp;</p>
<p>一、标准默认的W3C盒模型（content-box）</p>
<p>css设置的宽度是content的宽度，实际宽度 = css设置的宽度 + 左右填充 + 左右边框。</p>
<p>二、IE盒模型（border-box）</p>
<p>css设置的宽度是border及以内的宽度，设置的内填充、左右边框等等都会往里面压缩。</p>
<p>&nbsp;</p>
<h3>transition和animation的区别</h3>
<p>Animation和transition大部分属性是相同的，他们都是随时间改变元素的属性值。</p>
<p>1、transition需要触发一个事件才能改变属性，而animation不需要触发任何事件的情况下才会随时间改变属性值。</p>
<p>2、transition为2帧，从from .... to，而animation可以一帧一帧的</p>
<p>&nbsp;</p>
<h3>容器垂直居中</h3>
<p>一、margin-auto</p>
<p>父元素有宽高并设置相对定位，子元素有宽高并绝对定位。上下左右都为0，margin设置为auto</p>
<p>二、margin负值</p>
<p>父元素有宽高并设置相对定位，子元素有宽高并绝对定位。上50%，下50%；margin-top设置为 负子元素高度的一半，margin-left设置为 负子元素宽度的一半。</p>
<p>三、translate</p>
<p>父元素有宽高并设置相对定位，子元素有宽高并绝对定位。上50%，下50%；移动自身元素，transform:translate(-50%,-50%);</p>
<p>四、flex布局</p>
<p>父元素设置为display:flex，并且设置align-items:center ， justify-content:center</p>
<p>&nbsp;</p>
<h3>position定位</h3>
<p>默认static，没有定位</p>
<p>元素出现在正常的流中（忽略top, bottom, left, right 或者 z-index 声明）</p>
<p>&nbsp;</p>
<p>relative相对定位</p>
<p>1、使用了相对定位后，即使上下左右进行移动，原来的位置还会保留。</p>
<p>2、父元素使用相对定位后，子元素可以相对于父元素进行绝对定位</p>
<p>&nbsp;</p>
<p>absolute绝对定位</p>
<p>1、相对于最近的一个使用relative的元素进行定位，若都没有则相对于body定位</p>
<p>2、使用了绝对定位后，脱离文档流，自身原来的位置不会存在</p>
<p>&nbsp;</p>
<p>fixed固定定位</p>
<p>1、相对于浏览器窗口进行定位，定位后一直固定显示在的屏幕中，Fixed定位的元素和其他元素重叠。</p>
<p>2、脱离文档流，自身位置不存在</p>
<p>&nbsp;</p>
<p>sticky粘性定位</p>
<p>1、元素先按照普通文档流定位，然后相对于该元素在流中的flow root（BFC）和 containing block（最近的块级祖先元素）定位。</p>
<p>2、元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。</p>
<p>&nbsp;</p>
<p>inherit 继承定位</p>
<p>1、规定应该从父元素继承position 属性的值。</p>
<p>&nbsp;</p>
<h3>关于js动画和css3动画的差异性</h3>
<div>渲染线程分为main thread和compositor thread，如果css动画只改变transform和opacity，这时整个CSS动画得以在compositor trhead完成（而js动画则会在main thread执行，然后出发compositor thread进行下一步操作），特别注意的是如果改变transform和opacity是不会layout或者paint的。</div>
<p>区别：</p>
<p>功能涵盖面，js比css大</p>
<p>实现/重构难度不一，CSS3比js更加简单，性能跳优方向固定</p>
<p>对帧速表现不好的低版本浏览器，css3可以做到自然降级</p>
<p>css动画有天然事件支持</p>
<p>css3有兼容性问题</p>
<p>&nbsp;</p>
<h3>块元素和行元素</h3>
<div>块元素：独占一行，并且有自动填满父元素，可以设置margin和pading以及高度和宽度</div>
<p>行元素：不会独占一行，width和height会失效，并且在垂直方向的padding和margin会失<br />效。</p>
<p>&nbsp;</p>
<h3>浮动清除</h3>
<div>一、使用带clear属性的空元素</div>
<p>在浮动元素后使用一个空元素如&lt;div class="clear"&gt;&lt;/div&gt;，并在CSS中赋予.clear{clear:both;}属性即可清理浮动。亦可使用&lt;br class="clear" /&gt;或&lt;hr class="clear" /&gt;来进行清理。</p>
<p>&nbsp;</p>
<p>二、使用CSS的overflow属性</p>
<p>给浮动元素的容器添加overflow:hidden;或overflow:auto;可以清除浮动，另外在 IE6 中还需要触发 hasLayout ，例如为父元素设置容器宽高或设置 zoom:1。</p>
<p>在添加overflow属性后，浮动元素又回到了容器层，把容器高度撑起，达到了清理浮动的效果。</p>
<p>&nbsp;</p>
<p>三、给浮动的元素的容器添加浮动</p>
<p>给浮动元素的容器也添加上浮动属性即可清除内部浮动，但是这样会使其整体浮动，影响布局，不推荐使用。</p>
<p>&nbsp;</p>
<p>四、使用邻接元素处理</p>
<p>什么都不做，给浮动元素后面的元素添加clear属性。</p>
<p>&nbsp;</p>
<p>五、使用CSS的:after伪元素</p>
<p>结合:after 伪元素（注意这不是伪类，而是伪元素，代表一个元素之后最近的元素）和 IEhack ，可以完美兼容当前主流的各大浏览器，这里的 IEhack 指的是触发 hasLayout。</p>
<p>给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动</p>
<p>&nbsp;</p>
<h3>css3新特性</h3>
<p>CSS3边框如border-radius，box-shadow等；CSS3背景如background-size，background-origin等；CSS3 2D，3D转换如transform等；CSS3动画如animation等。</p>
<p>&nbsp;</p>
<h3>怎么样让一个元素消失</h3>
<div>1. opacity：0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如click事件，那么点击该区域，也能触发点击事件的</div>
<p>2. visibility：hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件</p>
<p>3. display：none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉。</p>
<p>&nbsp;</p>
<h3>display:none和visibilty:hidden的区别</h3>
<p>1. visibility：hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件</p>
<p>2. display：none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉</p>
<p>&nbsp;</p>
<h3>三栏布局的实现方式</h3>
<div>三列布局又分为两种，两列定宽一列自适应，以及两侧定宽中间自适应</div>
<div>&nbsp;</div>
<p>两列定宽一列自适应：</p>
<p>1、使用float+margin：</p>
<p>给div设置float：left，left的div添加属性margin-right：left和center的间隔px,right的div添加属性margin-left：left和center的宽度之和加上间隔</p>
<p>2、使用float+overflow：</p>
<p>给div设置float：left，再给right的div设置overflow:hidden。这样子两个盒子浮动，另一个盒子触发bfc达到自适应</p>
<p>&nbsp;</p>
<p>3、使用position：</p>
<p>父级div设置position：relative，三个子级div设置position：absolute，这个要计算好盒子的宽度和间隔去设置位置，兼容性比较好，</p>
<p>4、使用table实现：</p>
<p>父级div设置display：table，设置border-spacing：10px//设置间距，取值随意,子级div设置display:table-cell，这种方法兼容性好，适用于高度宽度未知的情况，但是margin失效，设计间隔比较麻烦，</p>
<p>5、flex实现：</p>
<p>parent的div设置display：flex；left和center的div设置margin-right；然后right 的div设置flex：1；这样子right自适应，但是flex的兼容性不好</p>
<p>6、grid实现：</p>
<p>parent的div设置display：grid，设置grid-template-columns属性，固定第一列第二列宽度，第三列auto，</p>
<p>&nbsp;</p>
<p>对于两侧定宽中间自适应的布局，对于这种布局需要把center放在前面，可以采用双飞翼布局：圣杯布局，来实现，也可以使用上述方法中的grid，table，flex，position实现</p>
<p>&nbsp;</p>
<h3>什么是BFC</h3>
<p>BFC也就是常说的块级格式化上下文，这是一个独立的渲染区域，规定了内部如何布局，并且这个区域的子元素不会影响到外面的元素，</p>
<p>其中比较重要的布局规则有内部box垂直放置，计算BFC的高度的时候，浮动元素也参与计算，触发BFC的规则有根元素，浮动元素，position为absolute或fixed的元素，display为inline-block，table-cell，table-caption，flex，inline-flex，overflow不为visible的元素</p>
<p>&nbsp;</p>
<p>//另外一个</p>
<p>&nbsp;</p>
<div>直译成：块级格式化上下文，是一个独立的渲染区域，并且有一定的布局规则。</div>
<p>BFC区域不会与float box重叠</p>
<p>BFC是页面上的一个独立容器，子元素不会影响到外面</p>
<p>计算BFC的高度时，浮动元素也会参与计算</p>
<p>那些元素会生成BFC：</p>
<p>根元素</p>
<p>float不为none的元素</p>
<p>position为fixed和absolute的元素</p>
<p>display为inline-block、table-cell、table-caption，flex，inline-flex的元素</p>
<p>overflow不为visible的元素</p>
<p>&nbsp;</p>
<h3>overflow的原理</h3>
<div>要讲清楚这个解决方案的原理，首先需要了解块格式化上下文，块格式化上下文是CSS可视化渲染的一部分，它是一块区域，规定了内部块盒 的渲染方式，以及浮动相互之间的影响关系</div>
<p>当元素设置了overflow样式且值部位visible时，该元素就构建了一个BFC，BFC在计算高度时，内部浮动元素的高度也要计算在内，也就是说技术BFC区域内只有一个浮动元素，BFC的高度也不会发生塌缩，所以达到了清除浮动的目的，</p>
<p>&nbsp;</p>
<h3>z-index的定位方法</h3>
<p>z-index属性设置元素的堆叠顺序，拥有更好堆叠顺序的元素会处于较低顺序元素之前，z-index可以为负，且z-index只能在定位元素上奏效，该属性设置一个定位元素沿z轴的位置，如果为正数，离用户越近，为负数，离用户越远，它的属性值有auto，默认，堆叠顺序与父元素相等，number，inherit，从父元素继承z-index属性的值</p>
<p>&nbsp;</p>
<h3><span>知道属性选择器和伪类选择器的优先级吗</span></h3>
<p>优先级相同</p>
<p>&nbsp;</p>
<h3><span>inline-block，inline和block的区别；为什么img是inline还可以设置宽高</span></h3>
<div><span>Block是块级元素，其前后都会有换行符，能设置宽度，高度，margin / padding水平垂直方向都有效。</span></div>
<p><span>内联：设置宽度和高度无效，边距在正确方向上无效，padding在水平方向垂直方向都有效，前后无换行符</span></p>
<p><span>内联块：能设置宽度高度，边距/填充水平垂直方向都有效，前后无换行符</span></p>
<p>&nbsp;</p>
<h3><span>了解重绘和重排吗，知道如何去减少重绘和重排吗，让文档分开文档流有某种方法</span></h3>
<div><span>DOM的变化影响到了预算内宿的几何属性范围宽高，浏览器重新计算元素的几何属性，其他元素的几何属性也会受到影响，浏览器需要重新构造渲染书，这个过程称为重排，浏览器将受到影响的部分重新放置在屏幕上的过程称为重绘，引起重排重绘的原因有：</span></div>
<p><span>添加或删除可见的DOM元素，</span></p>
<p><span>元素尺寸位置的改变</span></p>
<p><span>浏览器页面初始化，</span></p>
<p><span>浏览器窗口大小发生改变，重排一定导致重绘，重绘不一定导致重排，</span></p>
<p><span>减少重绘重排的方法有：</span></p>
<p><span>不在布局信息改变时做DOM查询，</span></p>
<p><span>使用csstext，className一次性更改属性</span></p>
<p><span>使用碎片</span></p>
<p><span>对于多次重排的元素，可以说动画。使用绝对定位分开文档流，使其不影响其他元素</span></p>
<p>&nbsp;</p>
<p>//还有</p>
<p>&nbsp;</p>
<p>渲染 = 重排 + 重绘
</p>
<p>重排 = 计算网页中各个元素的位置关系
</p>
<p>重绘 = 获取元素的样式，将样式绘制到浏览器中</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>每一次dom的操作都会引发重排/重绘。
</p>
<p>引发重排必定引发重绘，引发重绘只是将该元素样式重新绘制一遍</p>
<p>&nbsp;</p>
<h3><span>CSS画正方体，三角形</span></h3>
<p><span>三角形</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">#triangle02{
width: 0;
height: 0;
border-top: 50px solid blue;
border-right: 50px solid red;
border-bottom: 50px solid green;
border-left: 50px solid yellow;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>正方形</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.front{
transform:translateZ(1em);
}
.bottom{
transform:rotateX(-90deg) translateZ(1em);
}
.top{
transform:rotateX(90deg) translateZ(1em);
}
.left{
transform:rotateY(-90deg) translateZ(1em);
}
.right{
transform:rotateY(90deg) translateZ(1em);
}
.back{
transform:translateZ(-1em);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>两个嵌套的div，position都是absolute，子div设置top属性，那么这个top是相对于父元素的哪个位置定位的。</h3>
<p>border内侧&nbsp;&nbsp;padding外侧</p>
<p>&nbsp;</p>
<h3>css布局</h3>
<div>六种布局方式总结：圣杯布局、双飞翼布局、Flex布局、绝对定位布局、表格布局、网格布局。</div>
<p>圣杯布局是指布局从上到下分为header、container、footer，然后container部分定为三栏布局。这种布局方式同样分为header、container、footer。圣杯布局的缺陷在于 center 是在 container 的padding中的，因此宽度小的时候会出现混乱。</p>
<p>双飞翼布局给center 部分包裹了一个 main 通过设置margin主动地把页面撑开。</p>
<p>Flex布局是由CSS3提供的一种方便的布局方式。</p>
<p>绝对定位布局是给container 设置position: relative和overflow: hidden，因为绝对定位的元素的参照物为第一个postion不为static的祖先元素。 left 向左浮动，right 向右浮动。center 使用绝对定位，通过设置left和right并把两边撑开。 center 设置top: 0和bottom: 0使其高度撑开。</p>
<p>表格布局的好处是能使三栏的高度统一。</p>
<p>网格布局可能是最强大的布局方式了，使用起来极其方便，但目前而言，兼容性并不好。网格布局，可以将页面分割成多个区域，或者用来定义内部元素的大小，位置，图层关系。</p>
<p>&nbsp;</p>
