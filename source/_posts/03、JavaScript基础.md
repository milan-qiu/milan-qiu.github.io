---
title: "03、JavaScript基础"
date: "2020-05-12 17:21:00"
tags:
categories:
description: >-
  get请求传参长度的误区 误区：我们经常说get请求参数的大小存在限制，而post请求的参数大小是无限制的。 实际上HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对get请求参数的限制是来源与浏览器或web服务器，浏览器或web服务器限制了url的长度。为了明确这个概念，我们必须再
---

<h3>get请求传参长度的误区</h3>
<div>误区：我们经常说get请求参数的大小存在限制，而post请求的参数大小是无限制的。</div>
<p>实际上HTTP 协议从未规定 GET/POST 的请求长度限制是多少。对get请求参数的限制是来源与浏览器或web服务器，浏览器或web服务器限制了url的长度。为了明确这个概念，我们必须再次强调下面几点:</p>
<p>HTTP 协议 未规定 GET 和POST的长度限制</p>
<p>GET的最大长度显示是因为 浏览器和 web服务器限制了 URI的长度</p>
<p>不同的浏览器和WEB服务器，限制的最大长度不一样</p>
<p>要支持IE，则最大长度为2083byte，若只支持Chrome，则最大长度 8182byte</p>
<h3>&nbsp;</h3>
<h3>get和post请求在缓存方面的区别</h3>
<div>post/get的请求区别，具体不再赘述。</div>
<p>补充补充一个get和post在缓存方面的区别：</p>
<p>get请求类似于查找的过程，用户获取数据，可以不用每次都与数据库连接，所以可以使用缓存。</p>
<p>post不同，post做的一般是修改和删除的工作，所以必须与数据库交互，所以不能使用缓存。因此get请求适合于请求缓存。</p>
<p>&nbsp;</p>
<h3>闭包</h3>
<p>闭包就是能够读取其他函数内部变量的函数，或者子函数在外调用，子函数所在的父函数的作用域不会被释放。</p>
<p>&nbsp;</p>
<h3>前端中的事件流</h3>
<div>HTML中与javascript交互是通过事件驱动来实现的，例如鼠标点击事件onclick、页面的滚动事件onscroll等等，可以向文档或者文档中的元素添加事件侦听器来预订事件。想要知道这些事件是在什么时候进行调用的，就需要了解一下&ldquo;事件流&rdquo;的概念。</div>
<p>什么是事件流：事件流描述的是从页面中接收事件的顺序,DOM2级事件流包括下面几个阶段。</p>
<p>事件捕获阶段</p>
<p>处于目标阶段</p>
<p>事件冒泡阶段</p>
<p>addEventListener：addEventListener&nbsp;是DOM2 级事件新增的指定事件处理程序的操作，这个方法接收3个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是true，表示在捕获阶段调用事件处理程序；如果是false，表示在冒泡阶段调用事件处理程序。</p>
<p>IE只支持事件冒泡。</p>
<p>&nbsp;</p>
<h3>如何让事件先冒泡后捕获</h3>
<p>在DOM标准事件模型中，是先捕获后冒泡。但是如果要实现先冒泡后捕获的效果，对于同一个事件，监听捕获和冒泡，分别对应相应的处理函数，监听到捕获事件，先暂缓执行，直到冒泡事件被捕获后再执行捕获之间。</p>
<p>&nbsp;</p>
<h3>&nbsp;说一下事件委托</h3>
<div>简介：事件委托指的是，不在事件的发生地（直接dom）上设置监听函数，而是在其父元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过判断事件发生元素DOM的类型，来做出不同的响应。</div>
<p>举例：最经典的就是ul和li标签的事件监听，比如我们在添加事件时候，采用事件委托机制，不会在li标签上直接添加，而是在ul父元素上添加。</p>
<p>好处：比较合适动态元素的绑定，新添加的子元素也会有监听函数，也可以有事件触发机制。</p>
<p>&nbsp;</p>
<h3>图片的懒加载和预加载</h3>
<div>预加载：提前加载图片，当用户需要查看时可直接从本地缓存中渲染。</div>
<p>懒加载：懒加载的主要目的是作为服务器前端的优化，减少请求数或延迟请求数。</p>
<p>&nbsp;</p>
<p>两种技术的本质：两者的行为是相反的，一个是提前加载，一个是迟缓甚至不加载。<br />懒加载对服务器前端有一定的缓解压力作用，预加载则会增加服务器前端压力。</p>
<p>&nbsp;</p>
<h3>&nbsp;mouseover和mouseenter的区别</h3>
<div>mouseover：当鼠标移入元素或其子元素都会触发事件，所以有一个重复触发，冒泡的过程。对应的移除事件是mouseout</div>
<p>mouseenter：当鼠标移除元素本身（不包含元素的子元素）会触发事件，也就是不会冒泡，对应的移除事件是mouseleave</p>
<p>&nbsp;</p>
<h3>js的new操作符做了哪些事情</h3>
<p>new 操作符新建了一个空对象，这个对象原型指向构造函数的prototype，执行构造函数后返回这个对象。</p>
<p>&nbsp;</p>
<h3>改变函数内部this指针的指向函数（bind，apply，call的区别）</h3>
<p>&nbsp;通过apply和call改变函数的this指向，他们两个函数的第一个参数都是一样的表示要改变指向的那个对象，第二个参数，apply是数组，而call则是arg1,arg2...这种形式。通过bind改变this作用域会返回一个新的函数，这个函数不会马上执行。</p>
<p>&nbsp;</p>
<h3>js的各种位置，比如clientHeight,scrollHeight,offsetHeight ,以及scrollTop, offsetTop,clientTop的区别？</h3>
<div>clientHeight：表示的是可视区域的高度，不包含border和滚动条</div>
<p>offsetHeight：表示可视区域的高度，包含了border和滚动条</p>
<p>scrollHeight：表示了所有区域的高度，包含了因为滚动被隐藏的部分。</p>
<p>clientTop：表示边框border的厚度，在未指定的情况下一般为0</p>
<p>scrollTop：滚动后被隐藏的高度，获取对象相对于由offsetParent属性指定的父坐标(css定位的元素或body元素)距离顶端的高度。</p>
<p>&nbsp;</p>
<h3>垃圾收集机制</h3>
<p>//释放无用的数据，回收内存。js是自动收集的，object-c是手动收集的</p>
<p><strong>自动收集：找出没用数据，打上标识，释放其内存，周期性执行。</strong></p>
<p>&nbsp;</p>
<p><strong>标识</strong>无用数据的策略</p>
<p><strong>标记清除</strong>：给所有的<strong>变量</strong>打上标记，去掉&nbsp; 环境中的变量，以及&nbsp; 被环境中引用的变量。</p>
<p><strong>引用计数：</strong>跟踪每个值被引用的次数，当引用次数变成0时，就会被回收。</p>
<p>当声明了一个变量并将一个引用类型赋值给该变量时，则这个值的引用次数就是1。</p>
<p>var xm = { name=&rsquo;123&prime;,age=&rsquo;14&rsquo; };&nbsp; &nbsp; &nbsp;//这样xm就是1</p>
<p>如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数就减1。</p>
<p>xm = {}; 或 xm = null;&nbsp; &nbsp; &nbsp; //这样就由原来的1再减1。1-1=0</p>
<p><strong>注意：当循环引用时，a中带有b，b中带有a，引用计数就永远回收不到。</strong>(ie9以下的DOM采用的是引用计数策略，原生对象是标记清除策略，两种对象相互调用，可能产生循环计数)</p>
<p>&nbsp;</p>
<h3>eval是做什么的</h3>
<p>它的功能是将对应的字符串解析成js并执行，应该避免使用js，因为非常消耗性能（2次，一次解析成js，一次执行）</p>
<p>&nbsp;</p>
<h3>如何理解前端模块化</h3>
<p>前端模块化就是复杂的文件编程一个一个独立的模块，比如js文件等等，分成独立的模块有利于重用（复用性）和维护（版本迭代），这样会引来模块之间相互依赖的问题，所以有了commonJS规范，AMD，CMD规范等等，以及用于js打包（编译等处理）的工具webpack</p>
<p>&nbsp;</p>
<h3>说一下Commonjs、AMD和CMD</h3>
<div>一个模块是能实现特定功能的文件，有了模块就可以方便的使用别人的代码，想要什么功能就能加载什么模块。</div>
<div>&nbsp;</div>
<p>Commonjs：开始于服务器端的模块化，同步定义的模块化，每个模块都是一个单独的作用域，模块输出，modules.exports，模块加载require()引入模块。</p>
<p>&nbsp;</p>
<p>AMD：中文名异步模块定义的意思。</p>
<p>requireJS实现了AMD规范，主要用于解决下述两个问题。</p>
<p>1.多个文件有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器</p>
<p>2.加载的时候浏览器会停止页面渲染，加载文件越多，页面失去响应的时间越长。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">语法：requireJS定义了一个函数define，它是全局变量，用来定义模块。
requireJS的例子：

</span><span style="color: #008000;">//</span><span style="color: #008000;">定义模块</span>
<span style="color: #000000;">
define([</span>'dependency'], <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
</span><span style="color: #0000ff;">var</span> name = 'Byron'<span style="color: #000000;">;
</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> printName(){
console.log(name);
}
</span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
printName: printName
};
});<br />
</span><span style="color: #008000;">//</span><span style="color: #008000;">加载模块</span>
<span style="color: #000000;">
require([</span>'myModule'], <span style="color: #0000ff;">function</span><span style="color: #000000;"> (my){
my.printName();
}<br />
requirejs定义了一个函数define,它是全局变量，用来定义模块：
define(id</span>?dependencies?<span style="color: #000000;">,factory)

在页面上使用模块加载函数：
require([dependencies],factory)；</span></pre>
</div>
<p>&nbsp;</p>
<p>总结AMD规范：require（）函数在加载依赖函数的时候是异步加载的，这样浏览器不会失去响应，它指定的回调函数，只有前面的模块加载成功，才会去执行。</p>
<p>因为网页在加载js的时候会停止渲染，因此我们可以通过异步的方式去加载js,而如果需要依赖某些，也是异步去依赖，依赖后再执行某些方法。</p>
<p>&nbsp;</p>
<h3>&nbsp;对象深度克隆的简单实现</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span><span style="color: #000000;"> deepClone(obj){
</span><span style="color: #0000ff;">var</span> newObj= obj <span style="color: #0000ff;">instanceof</span> Array ?<span style="color: #000000;"> []:{};
</span><span style="color: #0000ff;">for</span>(<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> obj){
</span><span style="color: #0000ff;">var</span> temple= <span style="color: #0000ff;">typeof</span> obj[item] == 'object' ?<span style="color: #000000;"> deepClone(obj[item]):obj[item];
newObj[item] </span>=<span style="color: #000000;"> temple;
}
</span><span style="color: #0000ff;">return</span><span style="color: #000000;"> newObj;
}</span></pre>
</div>
<p>ES5的常用的对象克隆的一种方式。注意数组是对象，但是跟对象又有一定区别，所以我们一开始判断了一些类型，决定newObj是对象还是数组~</p>
<p>&nbsp;</p>
<h3>实现一个once函数，传入函数参数只执行一次</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span><span style="color: #000000;"> ones(func){
</span><span style="color: #0000ff;">var</span> tag=<span style="color: #0000ff;">true</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
</span><span style="color: #0000ff;">if</span>(tag==<span style="color: #0000ff;">true</span><span style="color: #000000;">){
func.apply(</span><span style="color: #0000ff;">null</span><span style="color: #000000;">,arguments);
tag</span>=<span style="color: #0000ff;">false</span><span style="color: #000000;">;
}
</span><span style="color: #0000ff;">return</span><span style="color: #000000;"> undefined
}
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>将原生的ajax封装成promise</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span>  myNewAjax=<span style="color: #0000ff;">function</span><span style="color: #000000;">(url){
</span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise(<span style="color: #0000ff;">function</span><span style="color: #000000;">(resolve,reject){
</span><span style="color: #0000ff;">var</span> xhr = <span style="color: #0000ff;">new</span><span style="color: #000000;"> XMLHttpRequest();
xhr.open(</span>'get'<span style="color: #000000;">,url);
xhr.send(data);
xhr.onreadystatechange</span>=<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
</span><span style="color: #0000ff;">if</span>(xhr.status==200&amp;&amp;readyState==4<span style="color: #000000;">){
</span><span style="color: #0000ff;">var</span> json=<span style="color: #000000;">JSON.parse(xhr.responseText);
resolve(json)
}</span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span>(xhr.readyState==4&amp;&amp;xhr.status!=200<span style="color: #000000;">){
reject(</span>'error'<span style="color: #000000;">);
}
}
})
}</span></pre>
</div>
<p>&nbsp;</p>
