---
title: "03、jQuery事件"
date: "2020-03-14 12:28:00"
tags:
categories:
description: >-
  鼠标事件 click() //单击鼠标时触发 $('#bn').click(function(){ alert(12324); }); dblclick() //双击鼠标时触发 $('#bn').dblclick(function(){ alert(12324); }); mousedown() /
---

<h2>鼠标事件</h2>
<p>click()&nbsp; &nbsp; &nbsp;//单击鼠标时触发</p>
<div class="cnblogs_code">
<pre>$('#bn').click(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){

alert(</span>12324<span style="color: #000000;">);

});</span></pre>
</div>
<p>&nbsp;</p>
<p>dblclick()&nbsp; &nbsp; &nbsp;//双击鼠标时触发</p>
<div class="cnblogs_code">
<pre>$('#bn').dblclick(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>mousedown()&nbsp; &nbsp; &nbsp;//鼠标按下时触发</p>
<div class="cnblogs_code">
<pre>$('#bn').mousedown(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>mouseup()&nbsp; &nbsp; &nbsp;//鼠标松开时触发</p>
<div class="cnblogs_code">
<pre>$('#bn').mouseup(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>mouseenter()&nbsp; &nbsp; &nbsp;//鼠标进入时触发</p>
<div class="cnblogs_code">
<pre>$('#bn').mouseenter(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>mouseleave()&nbsp; &nbsp; &nbsp;//鼠标离开时触发</p>
<div class="cnblogs_code">
<pre>$('#bn').mouseleave(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>hover( [enter,] over )&nbsp; &nbsp; &nbsp;//鼠标经过时触发。一个参数时，进入和离开都触发第一个函数；两个函数时，进入触发第一个函数，离开触发第二个函数</p>
<div class="cnblogs_code">
<pre>$('#bn').hover(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
},</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(){

alert(</span>5678<span style="color: #000000;">);

});</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>不常用</strong></p>
<p>mouseover()&nbsp; &nbsp; &nbsp;//鼠标进入指定元素&nbsp; 及其子元素时&nbsp; 触发</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">如给div绑定，div里面有一个p，进入div时触发一次，进入p时再触发一次</span></pre>
</div>
<p>&nbsp;</p>
<p>mouseout()&nbsp; &nbsp; &nbsp;//鼠标离开指定元素&nbsp; 及其子元素时&nbsp; 触发</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">如给div绑定，div里面有一个p，</span>

<span style="color: #008000;">//</span><span style="color: #008000;">进入div后，再进p，触发一次（因为离开了div）</span>

<span style="color: #008000;">//</span><span style="color: #008000;">离开p后，来到div，触发一次（因为离开了p）</span>

<span style="color: #008000;">//</span><span style="color: #008000;">最后离开div后，触发一次</span></pre>
</div>
<p>&nbsp;</p>
<p>mousemove()&nbsp; &nbsp; &nbsp;//鼠标移动时触发（触发次数多）</p>
<div class="cnblogs_code">
<pre>$('#tt').mousemove(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>scroll()&nbsp; &nbsp; &nbsp;//当鼠标滚动 指定元素时触发</p>
<div class="cnblogs_code">
<pre>$('#tt').mousemove(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});

</span><span style="color: #008000;">//</span><span style="color: #008000;">给#tt设置固定高度，#tt里面内容一定要够多，给#tt设置overflow:auto（作用是内容溢出时产生滚动条）</span></pre>
</div>
<p>&nbsp;</p>
<h2>键盘事件</h2>
<p>keydown()&nbsp; &nbsp; &nbsp;//键盘按下时触发</p>
<div class="cnblogs_code">
<pre>$(document).keydown(<span style="color: #0000ff;">function</span>(){      <span style="color: #008000;">//</span><span style="color: #008000;">这里的function有个event参数，需要的时候可以接收</span>
alert(12324<span style="color: #000000;">);
});

</span><span style="color: #008000;">//</span><span style="color: #008000;">如果给某个div元素绑定键盘事件，但是div没有输入框等产生焦点的地方，那么绑定的事件就不会生效</span>

<span style="color: #008000;">//</span><span style="color: #008000;">打开网页时，焦点默认在document上</span></pre>
</div>
<p>&nbsp;</p>
<p>keyup()&nbsp; &nbsp; &nbsp;//键盘松开时触发</p>
<div class="cnblogs_code">
<pre>$(document).keyup(<span style="color: #0000ff;">function</span>(){      <span style="color: #008000;">//</span><span style="color: #008000;">这里的function有个event参数，需要的时候可以接收</span>
alert(12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>不常用（慎用）</strong></p>
<p>keypress()&nbsp; &nbsp; &nbsp;//键盘按下时触发（兼容旧版浏览器）</p>
<div class="cnblogs_code">
<pre>$(document).keypress(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
alert(</span>12324<span style="color: #000000;">);
});</span></pre>
</div>
<p>缺点：</p>
<p>//对中文输入法支持不好，无法响应中文输入</p>
<p>//无法响应系统功能键（如delete、backspace等等）</p>
<p>//keyCode与keydown和keyup不是很一致</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>其它事件</h2>
<p>ready(fn)&nbsp; &nbsp; &nbsp;//当某元素载入就绪后，执行fn函数</p>
<div class="cnblogs_code">
<pre>$(document).ready(<span style="color: #0000ff;">function</span>(){  <span style="color: #008000;">//</span><span style="color: #008000;">code  });     //当DOM载入就绪后，执行函数里面的内容</span></pre>
</div>
<p>&nbsp;</p>
<p>resize()&nbsp; &nbsp; &nbsp;//当调整浏览器窗口大小时发生改变</p>
<div class="cnblogs_code">
<pre>$(window).resize(<span style="color: #0000ff;">function</span>(){ alert(123); });     <span style="color: #008000;">//</span><span style="color: #008000;">resize常用window搭配使用，换成其他对象则可能不生效。</span></pre>
</div>
<p>&nbsp;</p>
<p>focus()&nbsp; &nbsp; &nbsp;//获得焦点时触发</p>
<div class="cnblogs_code">
<pre>$('input').focus(<span style="color: #0000ff;">function</span>(){ console.log('获得焦点'); });    <span style="color: #008000;">//</span><span style="color: #008000;">通常与input搭配使用</span></pre>
</div>
<p>&nbsp;</p>
<p>blur()&nbsp; &nbsp; &nbsp; //失去焦点时触发</p>
<div class="cnblogs_code">
<pre>$('input').blur(<span style="color: #0000ff;">function</span>(){ console.log('失去获得焦点'); });    <span style="color: #008000;">//</span><span style="color: #008000;">通常与input搭配使用</span></pre>
</div>
<p>&nbsp;</p>
<p>change()&nbsp; &nbsp; &nbsp;//当某元素发生改变后触发</p>
<div class="cnblogs_code">
<pre>$('input').change(<span style="color: #0000ff;">function</span>(){ console.log('value发生了改变'); });    <span style="color: #008000;">//</span><span style="color: #008000;">通常与input搭配使用</span></pre>
</div>
<p>&nbsp;</p>
<p>select()&nbsp; &nbsp; //当某编辑框 内容被选中后触发</p>
<div class="cnblogs_code">
<pre>$('input').select(<span style="color: #0000ff;">function</span>(){ console.log('内容被选中了'); });    <span style="color: #008000;">//</span><span style="color: #008000;">一般与input、textarea等搭配使用</span></pre>
</div>
<p>&nbsp;</p>
<p>submit()&nbsp; &nbsp; //当提交表单时，发生submit事件</p>
<p>提交表单</p>
<div class="cnblogs_code">
<pre>&lt;input type="button" value="按钮"&gt;       <span style="color: #008000;">//</span><span style="color: #008000;">默认不可以提交，但是加了submit方法之后就可以了</span>
<span style="color: #000000;">
$(</span>'input[type=button]').submit();</pre>
</div>
<p>阻止表单提交</p>
<div class="cnblogs_code">
<pre>$('input[type=button]').submit(<span style="color: #0000ff;">function</span>(){  <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span>;  });      <span style="color: #008000;">//</span><span style="color: #008000;">只要在submit回调函数中返回false就可以阻止表单提交</span></pre>
</div>
<p>提交表单时还可以做其他事情（如一些简单的验证）</p>
<div class="cnblogs_code">
<pre>$('input[type=button]').submit(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){

</span><span style="color: #0000ff;">if</span>(a==b) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span>;     <span style="color: #008000;">//</span><span style="color: #008000;">如果a等于b，表单就不能提交</span>
<span style="color: #000000;">
});</span></pre>
</div>
<p>注：在form中默认提交表单的方式</p>
<p>1、&lt;input type = "submit" &gt;</p>
<p>2、&lt;button&gt;提交&lt;/button&gt;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>事件参数</h2>
<p>有些事件，如mousemove和keypress，我们需要获取鼠标的位置和按键的值，否则监听这些使劲按就没有什么意义了。</p>
<p>&nbsp;</p>
<p>event()</p>
<p>所有事件都会传入event对象作为参数，可以从event对象上获取到更多的信息。如：</p>
<div class="cnblogs_code">
<pre>$(document).keydown( <span style="color: #0000ff;">function</span><span style="color: #000000;">(event){

console.log( event.keyCode );     </span><span style="color: #008000;">//</span><span style="color: #008000;">打印出按键的keyCode</span>
<span style="color: #000000;">
} );

</span><span style="color: #008000;">//</span><span style="color: #008000;">除了keyCode外还有其他属性</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>事件绑定与取消</h2>
<p>on( events,[selector,] [data,] fn )&nbsp; &nbsp; &nbsp; &nbsp;//事件绑定（绑定一个或多个事件处理函数）</p>
<p>&nbsp;</p>
<p>绑定一个事件的事件处理函数，如：</p>
<div class="cnblogs_code">
<pre>一般形式：$('input').focus(<span style="color: #0000ff;">function</span>(){ console.log('获得焦点'<span style="color: #000000;">); });

on形式：   $(document).on( </span>'focus', 'input', <span style="color: #0000ff;">function</span>(){ console.log('获得焦点'); } );</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>绑定多个事件的事件处理函数，如：</p>
<div class="cnblogs_code">
<pre>$('a'<span style="color: #000000;">).add(document).on({
mouseenter : </span><span style="color: #0000ff;">function</span>(){},      <span style="color: #008000;">//</span><span style="color: #008000;">给a标签绑定的事件</span>
keydown      : <span style="color: #0000ff;">function</span>(){}       <span style="color: #008000;">//</span><span style="color: #008000;">给document绑定的事件</span>
});</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">events表示：事件类型</span>

<span style="color: #008000;">//</span><span style="color: #008000;">fn表示：执行函数</span>

<span style="color: #008000;">//</span><span style="color: #008000;">selector(可选)表示：选择器元素。//好处：这里的选择器可以js动态生成</span>

<span style="color: #008000;">//</span><span style="color: #008000;">data(可选)表示：传给事件处理函数的值</span></pre>
</div>
<p>&nbsp;</p>
<p>off( events,[selector],[fn] )&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;//事件取消（在选择元素上移除一个或多个事件的事件处理函数）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">只有用on绑定事件，才能用off移除</span>
<span style="color: #000000;">
函数：</span><span style="color: #0000ff;">function</span> foc () {  console.log('获得焦点'<span style="color: #000000;">);  }

绑定：$(document).on(</span>'focus','input'<span style="color: #000000;">,foc);

取消：$(document).off( </span>'focus' , 'input',foc );</pre>
</div>
<p>&nbsp;</p>
<p>one( events,[selector],[fn] )&nbsp; &nbsp; &nbsp; &nbsp; //事件绑定一次（绑定一个 一次性 的事件处理函数）</p>
<div class="cnblogs_code">
<pre>函数        ：<span style="color: #0000ff;">function</span> foc () {  console.log('获得焦点'<span style="color: #000000;">);  }

绑定一次：$(document).one(</span>'focus','input',foc);       <span style="color: #008000;">//</span><span style="color: #008000;">事件只会执行一次</span></pre>
</div>
<p>&nbsp;</p>
