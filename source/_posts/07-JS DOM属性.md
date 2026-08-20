---
title: "07-JS DOM属性"
date: "2020-01-22 15:06:00"
tags:
categories:
description: >-
  固有属性（property） 自定义属性（atrributes） <div id="ml" xx="xx" a="b"> 获取div的xx属性值 console.log(div.attributes.getNamedIteam('xx').nodeValue); console.log(div.at
---

<h2>&nbsp;</h2>
<p><strong><span style="font-size: 18pt; font-family: 幼圆;">固有属性（property）</span></strong></p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 18pt;">自定义属性（atrributes）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div   </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="ml"   </span><span style="color: #ff0000;">xx</span><span style="color: #0000ff;">="xx"   </span><span style="color: #ff0000;">a</span><span style="color: #0000ff;">="b"</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>获取div的xx属性值</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">console.log(div.attributes.getNamedIteam('xx').nodeValue);

console.log(div.attributes.['xx'].nodeValue);</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>删除div的xx属性值</strong></span></p>
<div class="cnblogs_code">
<pre>div.attributes.removeNamedIteam('xx');</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>创建div的yy属性</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span>  attr =<span style="color: #000000;"> document.createAttribute('yy');

attr.value </span>=<span style="color: #000000;"> 'bbq' ;

div.attributes.setNamedIteam(attr);</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-size: 18pt;"><strong><span style="font-family: 幼圆;">布尔属性</span></strong></span></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type </span><span style="color: #0000ff;">= "checkbox"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">北京
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type </span><span style="color: #0000ff;">= "checkbox" </span><span style="color: #ff0000;">checked</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">上海
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type </span><span style="color: #0000ff;">="checkbox"</span><span style="color: #0000ff;">&gt;</span>广州</pre>
</div>
<p><strong>除了用checked选中外，还可以</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> inputs =<span style="color: #000000;"> document.qureySelectorAll("input");

inputs[</span>1].checked = 1 ;    <span style="color: #008000;">//</span><span style="color: #008000;">只要令该表达式为真就可以被选中</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">select </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="city" </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="city"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="北京"</span><span style="color: #0000ff;">&gt;</span>  北京 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="上海" </span><span style="color: #ff0000;">selected</span><span style="color: #0000ff;">&gt;</span>  上海 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="广州"</span><span style="color: #0000ff;">&gt;</span>  广州 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><strong>除了用selected选中外，还可以</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> city =<span style="color: #000000;"> document.getElementById("city");
</span><span style="color: #0000ff;">var</span> options =<span style="color: #000000;"> city.options;
options[</span>1].selected = <span style="color: #0000ff;">true</span>;       <span style="color: #008000;">//</span><span style="color: #008000;">只要令该表达式为真就可以被选中</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>国籍：<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text" </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="中国" </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="country" </span><span style="color: #ff0000;">readonly</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><strong>除了用readonly外，还可以</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> country =<span style="color: #000000;"> document.getElementById("country");

country.readOnly </span>= <span style="color: #0000ff;">true</span>;      <span style="color: #008000;">//</span><span style="color: #008000;">只要令该表达式为真就变成只读</span></pre>
</div>
<p><strong>readonly跟disable的区别</strong></p>
<div class="cnblogs_code">
<pre>readonly可以提交到后端，disable不可以</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">select </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="city" </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="city" </span><span style="color: #ff0000;">multiple</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="北京"</span><span style="color: #0000ff;">&gt;</span>  北京 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="上海"</span><span style="color: #0000ff;">&gt;</span>  上海 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="广州"</span><span style="color: #0000ff;">&gt;</span>  广州 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><strong>除了用multiple实现多选外，还可以</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> city =<span style="color: #000000;"> document.getElementById("city");

city.multiple </span>= <span style="color: #0000ff;">true</span>;       <span style="color: #008000;">//</span><span style="color: #008000;">只要令该表达式为真就可以实现多选</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="uu" </span><span style="color: #ff0000;">hidden</span><span style="color: #0000ff;">&gt;</span>文字文字文字<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><strong>除了用hidden进行隐藏外，还可以</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> uu =<span style="color: #000000;"> document.getElementById("uu");

uu.hidden </span>= <span style="color: #0000ff;">true</span>;     <span style="color: #008000;">//</span><span style="color: #008000;">只要令该表达式为真就可以实现隐藏</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-size: 18pt;"><strong><span style="font-family: 幼圆;">字符串属性</span></strong></span></p>
<p><span style="font-size: 16px;"><strong><span style="font-family: 幼圆;">常见的字符串属性</span></strong></span></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>id、title、href、src、lang、dir、accesskey、name、value、class</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">W3C全局属性</span></strong></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>accesskey、class、contenteditable、dir、hidden、id、lang、spellcheck、style、tabindex、title、translate</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-size: 18pt;"><strong><span style="font-family: 幼圆;">data属性</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">button </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="btn" </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="button" </span><span style="color: #ff0000;">data-toggle</span><span style="color: #0000ff;">="12345&Prime; </span><span style="color: #ff0000;">data-xx-yy</span><span style="color: #0000ff;">="67890&Prime;</span><span style="color: #0000ff;">&gt;</span>按钮<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">buttom</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><span style="font-size: 16px; font-family: 幼圆;"><strong>获取data属性的值</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> btn =<span style="color: #000000;"> document.getElementById("btn");

console.log(btn.dataset.toggle);   </span><span style="color: #008000;">//</span><span style="color: #008000;">根据data-后面的名字获取</span>
<span style="color: #000000;">
console.log(btn.dataset.xxYy);     </span><span style="color: #008000;">//</span><span style="color: #008000;">如果data后面有两个-，那么采用驼峰形式的来获取</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-size: 18pt;"><strong><span style="font-family: 幼圆;">class属性（classList方法）</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">=" </span><span style="color: #ff0000;">aaa bbb ccc "</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>&nbsp;</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>获取class各个属性名,用数组的形式输出</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> CC =<span style="color: #000000;"> {

getClass : </span><span style="color: #0000ff;">function</span><span style="color: #000000;">(ele){

</span><span style="color: #0000ff;">return</span> ele.className.replace(/\s+/<span style="color: #000000;">, " ").split(" ");

}

}

</span><span style="color: #0000ff;">var</span> body =<span style="color: #000000;"> document.body;

console.log(CC.getClass(body));</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>判断&nbsp; 元素对象的className&nbsp; 是否存在</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> CC =<span style="color: #000000;"> {

hasClass : </span><span style="color: #0000ff;">function</span><span style="color: #000000;">(ele,cls){

</span><span style="color: #008000;">//</span><span style="color: #008000;">方法一</span>

<span style="color: #008000;">//</span><span style="color: #008000;">return -1 &lt; (" " + ele.className + " ").indexOf(" " + cls + " ");</span>

<span style="color: #008000;">//</span><span style="color: #008000;">方法二(classList方法)</span>

<span style="color: #0000ff;">return</span><span style="color: #000000;"> ele.classList.contains(cls);

}

}

</span><span style="color: #0000ff;">var</span> body =<span style="color: #000000;"> document.body;

console.log(CC.hasClass(body,'bbb'));    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果bbb的类名存在则返回true</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>给元素对象添加一个新的className</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> CC =<span style="color: #000000;"> {

addClass : </span><span style="color: #0000ff;">function</span><span style="color: #000000;">(ele,cls){

</span><span style="color: #008000;">//</span><span style="color: #008000;">方法一</span>

<span style="color: #008000;">//</span><span style="color: #008000;">if ( !this.hasClass(ele,cls) )</span>

<span style="color: #008000;">//</span><span style="color: #008000;">ele.className += " " + cls;</span>

<span style="color: #008000;">//</span><span style="color: #008000;">方法二(classList方法)</span>
<span style="color: #000000;">
ele.classList.add(cls);

}

}

</span><span style="color: #0000ff;">var</span> body =<span style="color: #000000;"> docement.body;

CC.addClass(body,'ddd');     </span><span style="color: #008000;">//</span><span style="color: #008000;">如果body里面不存在ddd，则添加ddd类名</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>删除元素的类名</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> CC =<span style="color: #000000;"> {

removeClass : </span><span style="color: #0000ff;">function</span><span style="color: #000000;">(ele,cls){

</span><span style="color: #008000;">//</span><span style="color: #008000;">方法一</span>

<span style="color: #008000;">//</span><span style="color: #008000;">if ( this.hasClass(ele,cls) )</span>

<span style="color: #008000;">//</span><span style="color: #008000;">var reg = new RegExp( '(\\s|^)' + cls + '(\\s|$)' , "gi" );</span>

<span style="color: #008000;">//</span><span style="color: #008000;">ele.className = ele.className.replace(reg, " ");</span>

<span style="color: #008000;">//</span><span style="color: #008000;">方法二(classList方法)</span>
<span style="color: #000000;">
ele.classList.remove(cls);

}

}

</span><span style="color: #0000ff;">var</span> body =<span style="color: #000000;"> document.body;

CC.removeClass(body,'aaa');    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果body里面存在aaa，则删除掉</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>元素类名 存在就删除，不存在就添加</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> CC =<span style="color: #000000;"> {

toggleClass : </span><span style="color: #0000ff;">function</span><span style="color: #000000;">(ele,cls){

</span><span style="color: #008000;">//</span><span style="color: #008000;">方法一</span>

<span style="color: #008000;">//</span><span style="color: #008000;">if ( this.hasClass(ele,cls) )</span>

<span style="color: #008000;">//</span><span style="color: #008000;">{</span>

<span style="color: #008000;">//</span><span style="color: #008000;">this.remove(ele,cls);</span>

<span style="color: #008000;">//</span><span style="color: #008000;">}else{</span>

<span style="color: #008000;">//</span><span style="color: #008000;">this.addClass(ele,cls);</span>

<span style="color: #008000;">//</span><span style="color: #008000;">}</span>

<span style="color: #008000;">//</span><span style="color: #008000;">方法二(classList方法)</span>

<span style="color: #0000ff;">return</span><span style="color: #000000;"> ele.classList.toggle(cls);

}

}

</span><span style="color: #0000ff;">var</span> body =<span style="color: #000000;"> document.body;

CC.toggleClass(body,'aaa');     </span><span style="color: #008000;">//</span><span style="color: #008000;">如果aaa存在执行删除，不存在执行添加</span></pre>
</div>
