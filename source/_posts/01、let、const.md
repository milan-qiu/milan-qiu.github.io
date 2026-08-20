---
title: "01、let、const"
date: "2020-04-22 13:00:00"
tags:
categories:
description: >-
  ECMAScript 与 JavaScript 的关系 ES是JS的标准，JS是ES的实现。 浏览器对新标准的支持 http://kangax.github.io/compat-table/es6/ let let与var的区别 1、let声明的变量，只在当前(块级)作用域内有效。 //块级作用域通
---

<h3>ECMAScript 与 JavaScript 的关系</h3>
<p>ES是JS的标准，JS是ES的实现。</p>
<h3>浏览器对新标准的支持</h3>
<p><a href="http://kangax.github.io/compat-table/es6/" target="_blank">http://kangax.github.io/compat-table/es6/</a></p>
<p>&nbsp;</p>
<h2>let</h2>
<h3>let与var的区别</h3>
<p>1、let声明的变量，只在当前(块级)作用域内有效。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">块级作用域通俗的说就是 { } 包起来的内容。但是当声明是对象时，{}里面就不是块级作用域，而是对象</span><span style="color: #008000;">
//</span><span style="color: #008000;">记得es5是没有块级作用域的</span><span style="color: #008000;">
//</span><span style="color: #008000;">for循环中()为一块级作用域，{}为二块级作用域，一块级包含二块级。</span></pre>
</div>
<p>&nbsp;</p>
<p>2、let声明的变量不能被重复命名</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">var的时候</span>
<span style="color: #0000ff;">var</span> a= 1<span style="color: #000000;">;
</span><span style="color: #0000ff;">var</span> a = 2<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">那么a最后就是2</span>

<span style="color: #008000;">//</span><span style="color: #008000;">let的时候</span>
let a= 1<span style="color: #000000;">;
let a </span>= 2<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">这样会报错，因为let的变量只能声明一次</span></pre>
</div>
<p>&nbsp;</p>
<p>3、不存在变量提升</p>
<div class="cnblogs_code">
<pre>console.log(a); <span style="color: #008000;">//</span><span style="color: #008000;">这里a是可以获取到的，不过是undefined。let就没有这个特性</span>
<span style="color: #0000ff;">var</span> a = 123; </pre>
</div>
<p>&nbsp;</p>
<p>4、暂存死区</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">块级作用域中存在let、const声明的变量，这个变量一开始就会存在封闭的作用域</span>
let a = 1<span style="color: #000000;">;
{
    console.log(a);
    let a </span>= 2<span style="color: #000000;">;
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">这样就会报错</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;常见小例子</h3>
<p>生成10个按钮，点击对应的按钮，弹出对应的 1-10 的数字</p>
<p>var 方式</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">自执行的函数会形成一个独立的函数作用域</span><span style="color: #0000ff;">for</span>(var i = 1; i &lt;= 10; i++<span style="color: #000000;">){
    (</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(i){　　//这个i是接收传进来的i
        </span><span style="color: #0000ff;">var</span> btn = document.createElement('button'<span style="color: #000000;">);
        btn.innerText </span>=<span style="color: #000000;"> i;
        btn.addEventListener(</span>'click',<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
            alert(i);
        },</span><span style="color: #0000ff;">false</span><span style="color: #000000;">)
    })(i)   //这个i是for那里的i。从for传给匿名函数
}</span></pre>
</div>
<p>&nbsp;</p>
<p>let方式</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">for</span>(let i = 1; i &lt;= 10; i++<span style="color: #000000;">){
    </span><span style="color: #0000ff;">var</span> btn = document.createElement('button'<span style="color: #000000;">);
    btn.innerText </span>=<span style="color: #000000;"> i;
    btn.addEventListener(</span>'click',<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
        alert(i);
    },</span><span style="color: #0000ff;">false</span><span style="color: #000000;">)
    document.body.appendChild(btn);
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>const</h2>
<p>const是用来声明常量的，且声明时必须赋值。</p>
<p>特性与let相同，不能重复声明，不存在提升，只在当前作用域有效</p>
<p>&nbsp;</p>
<h3>引用类型常量（修改）</h3>
<p>常量的值是不可改变的，但当常量为引用类型的时候就可以更改（但不是完全地更改），如</p>
<div class="cnblogs_code">
<pre>const xiao = {     <span style="color: #008000;">//</span><span style="color: #008000;">声明一个引用类型的常量</span>
    name : 'xiao'<span style="color: #000000;">,
    age : </span>18<span style="color: #000000;">
}
console.log(xiao.name);  </span><span style="color: #008000;">//</span><span style="color: #008000;">输出引用类型的值</span>
<span style="color: #000000;">
xiao.name </span>= 'haha';      <span style="color: #008000;">//</span><span style="color: #008000;">更改引用类型的值</span>
console.log(xiao.name);     <span style="color: #008000;">//</span><span style="color: #008000;">更改成功</span>
<span style="color: #000000;">
xiao </span>= {}; <span style="color: #008000;">//</span><span style="color: #008000;">清空里面的数据就会失败。</span><span style="color: #008000;">
//</span><span style="color: #008000;">说明const声明的的常量，只能保证引用类型的地址不发生变化，但是里面的数据是可以变化的。</span></pre>
</div>
<p>&nbsp;</p>
<p>再如</p>
<div class="cnblogs_code">
<pre>const abb = []; <span style="color: #008000;">//</span><span style="color: #008000;">声明一个引用类型的常量</span>
<span style="color: #000000;">
abb.push(</span>2);    <span style="color: #008000;">//</span><span style="color: #008000;">给该里面填充数据</span>
<span style="color: #000000;">
console.log(abb); </span><span style="color: #008000;">//</span><span style="color: #008000;">填充成功</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;</h3>
<h3>引用类型常量（防止修改）&nbsp;</h3>
<p>防止常量为引用类型时被修改，如</p>
<div class="cnblogs_code">
<pre>const xiao =<span style="color: #000000;"> {
    name : </span>'xiao'<span style="color: #000000;">,
    age : </span>18<span style="color: #000000;">
}
Object.freeze(xiao);  </span><span style="color: #008000;">//</span><span style="color: #008000;">用Object.freeze将常量包起来。只要包起来了里面的值就不能增加、修改、删除等操作</span>
<span style="color: #000000;">
console.log(xiao.name); </span><span style="color: #008000;">//</span><span style="color: #008000;">没修改时的值</span>
<span style="color: #000000;">
xiao.name </span>= 'haha';      <span style="color: #008000;">//</span><span style="color: #008000;">这样进行修改，不会报错也不会成功</span>
console.log(xiao.name);     <span style="color: #008000;">//</span><span style="color: #008000;">这里的值也还是没修改的值</span>
<span style="color: #000000;">
xiao.address </span>= 'beijing'; <span style="color: #008000;">//</span><span style="color: #008000;">给引用类型的常量添加方法，不会报错也不会成功</span>
console.log(xiao.address);  <span style="color: #008000;">//</span><span style="color: #008000;">xiao.address的值为undefined</span></pre>
</div>
<p>&nbsp;</p>
<p>再如</p>
<div class="cnblogs_code">
<pre>const abb =<span style="color: #000000;"> [];

Object.freeze(abb);

abb.push(</span>2);  <span style="color: #008000;">//</span><span style="color: #008000;">这里就会报错了，原因看上个例子</span>
<span style="color: #000000;">
console.log(abb);</span></pre>
</div>
<p>&nbsp;</p>
<p>//Object.freeze(a);&nbsp; //a对象里面的值不能扩展、修改、删除等等</p>
<h3>&nbsp;</h3>
<h3>es6之前声明常量方法</h3>
<p>第一种</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> a = 123; <span style="color: #008000;">//</span><span style="color: #008000;">假装是常量的方式</span></pre>
</div>
<p>&nbsp;</p>
<p>第二种</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> b =<span style="color: #000000;"> {}; 

b.name </span>= 'xiaoming'<span style="color: #000000;">;  

</span><span style="color: #008000;">//</span><span style="color: #008000;">给对象添加常量。这个常量可以被修改、删除等操作</span></pre>
</div>
<p>&nbsp;</p>
<p>第三种</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">还有一个添加常量的方法。这个常量可以控制是否可写、可读</span>
<span style="color: #000000;">
Object.defineProperty(b,</span>'age',{  <br /><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数是表示要操作的对象。当然可以也可以为window，这样就会是一个全局的常量了<br />//第二个参数是属性名<br />//第三个参数是{}，里面是描述的操作</span>
<span style="color: #000000;">    
    value : </span>'18',    <span style="color: #008000;">//</span><span style="color: #008000;">value后面是 属性值</span><span style="color: #000000;">    
    writable : </span><span style="color: #0000ff;">false</span>;  <span style="color: #008000;">//</span><span style="color: #008000;">这里表示不可写，就是只读的意思</span>
})</pre>
</div>
<p>&nbsp;</p>
<p>上面第三种方法可以保证变量不被修改，但是对象还是可以正常的扩展的，如</p>
<div class="cnblogs_code">
<pre>b.sex = 'nan'<span style="color: #000000;">;
console.log(b.sex); </span><span style="color: #008000;">//</span><span style="color: #008000;">扩展是可以成功的</span></pre>
</div>
<p>&nbsp;</p>
<p>要想对象不能扩展，就得这样：</p>
<div class="cnblogs_code">
<pre>Object.seal(b); <span style="color: #008000;">//</span><span style="color: #008000;">表示b对象不能被扩展。位置放在刚定义完对象的时候</span></pre>
</div>
<p>&nbsp;</p>
<p>//Object.seal(b);&nbsp; //b对象里面的值不能阔在，但是可以修改。</p>
<p>第三种方法 +&nbsp;Object.seal()&nbsp; = Object.freeze()</p>
<p>.......</p>
