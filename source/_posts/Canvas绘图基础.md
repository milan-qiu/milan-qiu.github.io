---
title: "Canvas绘图基础"
date: "2020-04-13 13:18:00"
updated: "2020-04-13 20:35:00"
tags:
categories:
description: >-
  Canvas HTML5 <canvas> 元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成. <canvas> 标签只是图形容器，您必须使用脚本来绘制图形。 你可以通过多种方法使用 canvas 绘制路径,盒、圆、字符以及添加图像。 Canvas初始化 创建画布 canvas默认
---

<h2>Canvas</h2>
<p>HTML5 &lt;canvas&gt; 元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成.</p>
<p>&lt;canvas&gt; 标签只是图形容器，您必须使用脚本来绘制图形。</p>
<p>你可以通过多种方法使用 canvas 绘制路径,盒、圆、字符以及添加图像。</p>
<p>&nbsp;</p>
<h2>Canvas初始化</h2>
<h3>创建画布</h3>
<p>canvas默认画布大小：300*150px</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">canvas </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="myCanvas"</span><span style="color: #ff0000;"> width</span><span style="color: #0000ff;">="600px"</span><span style="color: #ff0000;"> height</span><span style="color: #0000ff;">="300px"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
    您的浏览器不支持canvas
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">canvas</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 画布的宽高在html标签，或js中定义 </span><span style="color: #008000;">--&gt;</span>
<span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 若在css中定义宽高，画布会按照比例缩放在css的框内 </span><span style="color: #008000;">--&gt;</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;用JavaScript绘制图像</h3>
<p>所有绘制工作都通过下面js来操作</p>
<div class="cnblogs_code">
<pre>&lt;script type="text/javascript"&gt;
    <span style="color: #0000ff;">var</span> myCanvas = document.getElementById('myCanvas');<span style="color: #008000;">/*</span><span style="color: #008000;">首先，找到 &lt;canvas&gt; 元素</span><span style="color: #008000;">*/</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">若在js中定义画布的宽高</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">myCanvas.width=300;</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">myCanvas.height=150;</span>
    <span style="color: #0000ff;">var</span> ctx = myCanvas.getContext('2d');<span style="color: #008000;">/*</span><span style="color: #008000;">然后，创建 context 对象</span><span style="color: #008000;">*/</span>
    <span style="color: #008000;">//</span><span style="color: #008000;"> getContext("2d") 对象是内建的 HTML5 对象，拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。</span>
&lt;/script&gt;</pre>
</div>
<h3><span style="font-size: 1.17em;">Canvas坐标</span></h3>
<p>canvas左上角坐标 (0,0)</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200412200719203-1506857102.png" alt="" /></p>
<p>&nbsp;</p>
<h2>Canvas基础绘图</h2>
<h3>画直线</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">先画好路径</span>
ctx.moveTo(0,0); <span style="color: #008000;">/*</span><span style="color: #008000;">起点坐标</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.lineTo(</span>200,100); <span style="color: #008000;">/*</span><span style="color: #008000;">终点坐标</span><span style="color: #008000;">*/</span>
<span style="color: #008000;">//</span><span style="color: #008000;">根据画好的路径开始描绘</span>
ctx.stroke(); /*默认用黑色线条画*/</pre>
</div>
<p>&nbsp;</p>
<p>//画第二个形状的时候，要先结束前面的路径 ctx.begginPath()，不然会画多一遍</p>
<div class="cnblogs_code">
<pre>ctx.beginPath(); <span style="color: #008000;">/*</span><span style="color: #008000;">结束前面路径</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.moveTo(</span>200,100<span style="color: #000000;">);
ctx.lineTo(</span>200,300<span style="color: #000000;">);
ctx.strokeStyle </span>= 'red';<span style="color: #008000;">/*</span><span style="color: #008000;">更换画笔颜色</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.stroke();</span></pre>
</div>
<p>&nbsp;</p>
<h3>闭合路径</h3>
<div class="cnblogs_code">
<pre>ctx.beginPath(); <span style="color: #008000;">/*</span><span style="color: #008000;">结束前面路径</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.moveTo(</span>200,100<span style="color: #000000;">);
ctx.lineTo(</span>200,250<span style="color: #000000;">);
ctx.lineTo(</span>50,250<span style="color: #000000;">);
ctx.closePath();  </span><span style="color: #008000;">/*</span><span style="color: #008000;">就是把几个点封闭起来</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.stroke();</span></pre>
</div>
<p>&nbsp;</p>
<h3>画圆</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">ctx.beginPath();
ctx.arc(</span>200,100,100,0,2*Math.PI,<span style="color: #0000ff;">true</span><span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">1、2参数定义圆心，3参数半径，3、4参数圆的起始弧度和终止弧度（完整的圆是0-2&Pi;），5参数是否逆时针画</span>
ctx.strokeStyle = 'green'<span style="color: #000000;">;
ctx.stroke();</span></pre>
</div>
<p>&nbsp;</p>
<h3>画矩形</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">ctx.beginPath();
ctx.strokeRect(</span>300,5,100,50);    <span style="color: #008000;">//</span><span style="color: #008000;">自带stroke方法</span><span style="color: #008000;">
//</span><span style="color: #008000;">1、2参数矩形左上角坐标，3、4参数矩形的宽高<br /><br />//ctx.strokeRect(300,5,100,50)； //意思是描边<br />//ctx.fillRect(300,5,100,50);   //意思是填充</span></pre>
</div>
<p>&nbsp;</p>
<h3>描边与填充</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">stroke（描边）</span>
ctx.moveTo(0,0<span style="color: #000000;">);
ctx.lineTo(</span>100,100<span style="color: #000000;">);
ctx.lineTo(</span>100,200<span style="color: #000000;">);
ctx.strokeStyle </span>= "cyan"; <span style="color: #008000;">/*</span><span style="color: #008000;">更换画笔</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.lineWidth </span>= 5; <span style="color: #008000;">/*</span><span style="color: #008000;">定义画条的粗细</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.stroke();  </span><span style="color: #008000;">/*</span><span style="color: #008000;">开始描边</span><span style="color: #008000;">*/</span>
        
<span style="color: #008000;">//</span><span style="color: #008000;">fill（填充）</span>
ctx.fillStyle = "black";<span style="color: #008000;">/*</span><span style="color: #008000;">填充的颜色</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.fill(); </span><span style="color: #008000;">/*</span><span style="color: #008000;">会以闭合的形式填充</span><span style="color: #008000;">*/</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>图形变换</h2>
<h3>平移</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//没画前</span><span style="color: #008000;">平移</span>
ctx.translate(0,100); <span style="color: #008000;">/*横坐标平移0，纵坐标平移100。</span><span style="color: #008000;">在没画之前，把坐标起始位置改变</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.moveTo(</span>0,0); <span style="color: #008000;">/*</span><span style="color: #008000;"> 坐标原点已经平移了，开始位置为(0,100) </span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.lineTo(</span>100,100<span style="color: #000000;">);
ctx.stroke();</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">画过程中平移</span>
ctx.moveTo(0,0);<span style="color: #008000;">/*</span><span style="color: #008000;">起点已经确认</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.translate(</span>0,100);<span style="color: #008000;">/*</span><span style="color: #008000;">本来终点的纵坐标已经确认为100，经过平移后纵坐标为200</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.lineTo(</span>100,100);<span style="color: #008000;">/*</span><span style="color: #008000;">实际终点坐标为(100,200)</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.stroke();</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">画之后平移</span>
ctx.moveTo(0,0);<span style="color: #008000;">/*</span><span style="color: #008000;">起点已经确认</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.lineTo(</span>100,100);<span style="color: #008000;">/*</span><span style="color: #008000;">终点确认</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.translate(</span>0,100);<span style="color: #008000;">/*</span><span style="color: #008000;">现在平移不会产生效果（起点终点已确认）。但是会影响后面的描边</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.stroke();</span></pre>
</div>
<h3>&nbsp;旋转</h3>
<p>//注意：之前的平移会决定后面的点</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">起点没有旋转的线</span>
ctx.moveTo(0,0<span style="color: #000000;">);
ctx.lineTo(</span>100,50<span style="color: #000000;">);
ctx.stroke();
                
</span><span style="color: #008000;">//</span><span style="color: #008000;">起始旋转45度的线</span>
<span style="color: #000000;">ctx.beginPath();
ctx.rotate(Math.PI </span>/ 4); <span style="color: #008000;">/*</span><span style="color: #008000;"> 圆点绕x轴旋转45度 </span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.moveTo(</span>0,0<span style="color: #000000;">);
ctx.lineTo(</span>100,50<span style="color: #000000;">);
ctx.strokeStyle </span>= 'red'<span style="color: #000000;">;
ctx.stroke();</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;缩放</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 缩放要在画之前决定好</span>
ctx.scale(1,0.5);<span style="color: #008000;">/*</span><span style="color: #008000;">横坐标不变，纵坐标缩放50%。</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.fillRect(</span>0,0,100,100);</pre>
</div>
<p>&nbsp;</p>
<h3>save和restore</h3>
<p>//作用：解决图形变换对后面操作的影响</p>
<p>//save和restore一定要成对出现才有效果</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">ctx.save(); //保存前面绘画环境，包括变换和样式<br />
</span><span style="color: #008000;">/*</span><span style="color: #008000;"> 里面可以做任何图形变换的操作... </span><span style="color: #008000;">*/<br /><br /></span><span style="color: #000000;">
ctx.restore(); //恢复之前保存的绘画环境，包括变换和样式<br />
</span><span style="color: #008000;">/*</span><span style="color: #008000;"> restore后面的任何操作，都不会受到图形变换的影响了 </span><span style="color: #008000;">*/</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;Canvas渐变</h2>
<h3>&nbsp;线性渐变</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">1、确认线条的位置</span>
<span style="color: #0000ff;">var</span> linearGradient = ctx.createLinearGradient(0,0,100,100<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建一个线性渐变从第一个点(0,0),到第二个点(100,100)做渐变</span>
        
<span style="color: #008000;">//</span><span style="color: #008000;">2、确认渐变的颜色（渐变至少有两种颜色）</span>
linearGradient.addColorStop(0,'red'); <span style="color: #008000;">//</span><span style="color: #008000;">0%的时候是红色</span>
linearGradient.addColorStop(.5,'blue');<span style="color: #008000;">//</span><span style="color: #008000;">50%的时候是蓝色</span>
linearGradient.addColorStop(1,'green'); <span style="color: #008000;">//</span><span style="color: #008000;">100%的时候是绿色</span>
        
<span style="color: #008000;">//</span><span style="color: #008000;">3、用渐变的颜色作为填充色</span>
ctx.fillStyle =<span style="color: #000000;"> linearGradient;
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">4、画一个矩形，并填充颜色</span>
ctx.fillRect(0,0,100,100);</pre>
</div>
<p>&nbsp;</p>
<h3>径向渐变&nbsp;</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">1、确认径向渐变的位置</span>
<span style="color: #0000ff;">var</span> radialGradient = ctx.createRadialGradient(200,200,0,200,200,100<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建一个径向渐变对象，前三个参数是一个圆的圆心半径，后三个参数是另一个圆的圆心半径</span>
                
<span style="color: #008000;">//</span><span style="color: #008000;">2、确认渐变的颜色（渐变至少有两种颜色）</span>
radialGradient.addColorStop(0,'red'); <span style="color: #008000;">//</span><span style="color: #008000;">0%的时候是红色</span>
radialGradient.addColorStop(.5,'blue');<span style="color: #008000;">//</span><span style="color: #008000;">50%的时候是蓝色</span>
radialGradient.addColorStop(1,'green'); <span style="color: #008000;">//</span><span style="color: #008000;">100%的时候是绿色</span>
                
<span style="color: #008000;">//</span><span style="color: #008000;">3、用渐变的颜色作为填充色</span>
ctx.fillStyle =<span style="color: #000000;"> radialGradient;
                
</span><span style="color: #008000;">//</span><span style="color: #008000;">4、画一个圆，并填充颜色</span>
ctx.arc(200,200,100,0,2*Math.PI,<span style="color: #0000ff;">true</span><span style="color: #000000;">);
ctx.fill();</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;Canvas文本</h2>
<h3>使用</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">1、设置文本</span>
<span style="color: #0000ff;">var</span> str = "你好啊！"<span style="color: #000000;">;
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">2、看需求设置文本样式（与css的font的使用一致）</span>
ctx.font = "50px 宋体"
        
<span style="color: #008000;">//</span><span style="color: #008000;">3、看需求设置水平对齐（用法如下图）</span>
ctx.textAlign = "center"<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">3、看需求设置垂直对齐（用法如下图）</span>
ctx.textBaseline = "top"<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">4、描边文本</span>
ctx.strokeText(str,100,100);<span style="color: #008000;">/*</span><span style="color: #008000;"> str表示需要描边的文本，(100,100)表示文本出现的位置 </span><span style="color: #008000;">*/</span>
<span style="color: #008000;">//</span><span style="color: #008000;">4、填充文本</span><span style="color: #008000;">
//</span><span style="color: #008000;">ctx.fillText(str,100,200);/* str表示需要填充的文本，(100,200)表示文本出现的位置 */</span></pre>
</div>
<p>&nbsp;//获取文本宽度：var width = ctx.measureText(str).width;</p>
<h3>&nbsp;textAlign</h3>
<h3><img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200413131615107-1029343624.png" alt="" /></h3>
<h3>&nbsp;textBaseline</h3>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200413131745857-120386116.png" alt="" /></p>
<h2>&nbsp;Canvas图像/视频</h2>
<h3>&nbsp;使用</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">1、创建图片对象</span>
<span style="color: #0000ff;">var</span> img = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Image();

</span><span style="color: #008000;">//</span><span style="color: #008000;">2、给img引入一张图片</span>
img.src = "./xx.png"<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">3、等待img对象加载完成后，再开始绘制</span>
img.onload = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">将引进来的图片绘制出来</span>
    ctx.drawImage(img,0,0); <span style="color: #008000;">/*</span><span style="color: #008000;"> 1参数是绘制的对象，2、3参数是从画布哪个位置开始绘 </span><span style="color: #008000;">*/</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;缩放</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">3、等待img对象加载完成后，再开始绘制</span>
img.onload = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">将引进来的图片绘制出来</span>
    ctx.drawImage(img,0,0,200,200<span style="color: #000000;">); 
    </span><span style="color: #008000;">/*</span><span style="color: #008000;"> 1参数是绘制的对象，2、3参数是从画布哪个位置开始绘 ,4、5参数是将图片缩放成200*200的像素 </span><span style="color: #008000;">*/</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>裁剪&nbsp;</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">3、等待img对象加载完成后，再开始绘制</span>
img.onload = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">将引进来的图片绘制出来</span>
    ctx.drawImage(img,0,0,200,200,0,0<span style="color: #000000;">); 
    </span><span style="color: #008000;">/*</span><span style="color: #008000;"> 1参数是绘制的对象，
    2、3参数开始裁剪的xy坐标点，
    4、5参数裁剪出来的图片的宽高，
    6、7参数从画布的哪个位置开始绘制</span><span style="color: #008000;">*/</span><span style="color: #000000;">
}<br />//若裁剪加缩放：可8、9参数指定裁剪出来的图像按照 xx*xx 的比例缩放。</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;图形画刷</h2>
<p>//将图片/视频当成颜色来填充</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">3、等待img对象加载完成后，再开始绘制</span>
img.onload = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">1、创建一个画刷对象</span>
    <span style="color: #0000ff;">var</span> pattern = ctx.createPattern(img,"repeat"<span style="color: #000000;">);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">1参数是当填充背景对象，2参数是该对象该怎样重复</span>
    
    <span style="color: #008000;">//</span><span style="color: #008000;">2、把填充的颜色换成img对象</span>
    ctx.fillStyle =<span style="color: #000000;"> pattern;
    
    </span><span style="color: #008000;">//</span><span style="color: #008000;">3、尝试填充到矩形里面</span>
    ctx.fillRect(0,0,200,200<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>&nbsp;剪辑区域</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">ctx.save();
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">1、先定义一个形状</span>
ctx.arc(300,100,200,0,Math.PI*2,<span style="color: #0000ff;">true</span><span style="color: #000000;">);
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">2、只要在该形状里面才会被显示</span>
<span style="color: #000000;">ctx.clip();
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">3、随便描边/填充一个形状</span>
ctx.fillRect(100,100,200,200<span style="color: #000000;">);
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">4、剪辑操作要在save、restore里面，不然会影响后续描边/填充操作</span>
ctx.restore();</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>阴影绘制&nbsp;</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">ctx.save();
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">1、阴影的具体设置</span>
ctx.shadowOffsetX = 10;    <span style="color: #008000;">/*</span><span style="color: #008000;">阴影的X偏移</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.shadowOffsetY </span>= 10;    <span style="color: #008000;">/*</span><span style="color: #008000;">阴影的Y偏移</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.shadowColor </span>= "rgba(0,0,0,.5)";    <span style="color: #008000;">/*</span><span style="color: #008000;">阴影的颜色</span><span style="color: #008000;">*/</span><span style="color: #000000;">
ctx.shadowBlur </span>= 10;    <span style="color: #008000;">/*</span><span style="color: #008000;">阴影的模糊程度</span><span style="color: #008000;">*/</span>
        
<span style="color: #008000;">//</span><span style="color: #008000;">2、随便填充一个形状</span>
ctx.fillRect(0,0,100,100<span style="color: #000000;">);
        
</span><span style="color: #008000;">//</span><span style="color: #008000;">3、所有的操作都要在save、restore里面完成，不然所有绘制的图像都会有阴影</span>
ctx.restore();</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;绘制曲线</h2>
<h3>&nbsp;圆弧</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">圆弧</span>
ctx.arc(100,100,80,0,Math.PI,<span style="color: #0000ff;">true</span>);    <span style="color: #008000;">//</span><span style="color: #008000;">逆时针画半圆弧</span>
ctx.stroke();    <span style="color: #008000;">//</span><span style="color: #008000;">将半圆弧 描/填充 出来</span></pre>
</div>
<h3>&nbsp;</h3>
<h3>二次贝塞尔曲线 （二次样条曲线）</h3>
<p>//在线曲线生成工具：<a href="http://blogs.sitepointstatic.com/examples/tech/canvas-curves/quadratic-curve.html" target="_blank">http://blogs.sitepointstatic.com/examples/tech/canvas-curves/quadratic-curve.html</a></p>
<p>//生成后，复制beginPath下面代码即可。</p>
<p>&nbsp;</p>
<h3>三次贝塞尔曲线</h3>
<p>//在线曲线生成工具：<a href="http://blogs.sitepointstatic.com/examples/tech/canvas-curves/bezier-curve.html" target="_blank">http://blogs.sitepointstatic.com/examples/tech/canvas-curves/bezier-curve.html</a></p>
<p>//使用方法同上。</p>
<p>&nbsp;</p>
<h2>Canvas动画</h2>
<p>/* coding */</p>
<h2>Canvas离屏技术</h2>
<p>/* coding */</p>
<p>&nbsp;</p>
