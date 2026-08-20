---
title: "05、JSON与AJAX基础"
date: "2020-03-14 12:43:00"
updated: "2020-03-14 22:36:00"
tags:
categories:
description: >-
  Ajax 什么是Ajax？([ˈeɪdʒæks]) Ajax的全称是 Asynchronous JavaScript and XML（即异步的JavaScript和XML），它并不是一种新的编程语言，而是几种原有技术的结合体。 Ajax有什么用？ Ajax是一种无需重新加载整个网页的情况下，能够更新
---

<h2>Ajax</h2>
<h3>什么是Ajax？([ˈeɪdʒ&aelig;ks])</h3>
<p>Ajax的全称是 Asynchronous JavaScript and XML（即异步的JavaScript和XML），它并不是一种新的编程语言，而是几种原有技术的结合体。</p>
<p>&nbsp;</p>
<h3>Ajax有什么用？</h3>
<p>Ajax是一种无需重新加载整个网页的情况下，能够更新部分网页的技术。</p>
<p>&nbsp;</p>
<h3>Ajax的优点</h3>
<p>1、通过异步模式，提升了用户体验。</p>
<p>2、优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用。</p>
<p>3、Ajax引擎在客户端运行，承担了一部分本来由服务器承担的工作，从而减少了大用户量下的服务器负载。</p>
<p>&nbsp;</p>
<h3>Ajax的缺点</h3>
<p>1、不支持浏览器back按钮。</p>
<p>2、安全问题Ajax暴露了与服务器交互的细节。</p>
<p>3、对搜索引擎的支持比较弱。</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>XMLHttpRequest对象</h2>
<h3>什么是XMLHttpRequest？</h3>
<p>是一种支持异步请求的技术，它是Ajax的核心。</p>
<p>&nbsp;</p>
<h3>XMLHttpRequest的作用</h3>
<p>1、可以向服务器提出请求并处理响应，而不阻塞用户。</p>
<p>2、可以在页面加载以后进行页面的局部更新。</p>
<p>&nbsp;</p>
<h2>如何使用Ajax？</h2>
<p>要完整实现一个Ajax异步调用和局部刷新，通常需要以下几个步骤：</p>
<p>1、创建XMLHttpRequest对象，也就是创建一个异步调用对象</p>
<p>2、创建一个新的HTTP请求，并指定该HTTP请求的方法、URL</p>
<p>3、设置响应HTTP请求状态变化的函数</p>
<p>4、发送HTTP请求</p>
<p>5、获取异步调用返回的数据</p>
<p>6、使用Javascript和DOM&nbsp; 实现局部刷新</p>
<p>如：</p>
<p><strong>1、创建XMLHttpRequest对象</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span><span style="color: #000000;"> xmlhttp;
</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (window.XMLHttpRequest) {
</span><span style="color: #008000;">//</span><span style="color: #008000;">主流浏览器、IE7+</span>
xmlhttp = <span style="color: #0000ff;">new</span><span style="color: #000000;"> XMLHttpRequest;
} </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
</span><span style="color: #008000;">//</span><span style="color: #008000;">IE6/IE5</span>
xmlhttp = <span style="color: #0000ff;">new</span> ActiveXObject("Microsoft.XMLHTTP"<span style="color: #000000;">);
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">console.log(xmlhttp);</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>2、创建一个新的HTTP请求</strong></p>
<div class="cnblogs_code">
<pre>xmlhttp.open( "post" , "./server.php" , <span style="color: #0000ff;">true</span> );</pre>
</div>
<p>&nbsp;</p>
<p><strong>open(method,url,async)</strong>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;//创建HTTP请求，规定请求的类型、URL以及 是否为异步处理请求</p>
<p>method：请求类型，GET或POST</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">与post相比，get更简单也更快，并且在大部分情况下都能用，然而，在以下情况中，必须使用post请求：<br />1、无法使用缓存文件（更新服务器上的文件或数据库）<br />2、向服务器发送大量数据（post没有数据量限制）<br />3、发送包含未知字符的用户输入时，post比get更稳定也更可靠。</span></pre>
</div>
<p>url：文件在服务器上的位置</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">url是open()方法的一个必选参数，用来设置服务器上文件的地址，该文件可以是任何类型的文件，如.txt、.xml等，或者服务器脚本文件：.asp、.php（在传回响应之前，能够在服务器上执行任务）等等。</span></pre>
</div>
<p>async：true（异步）或false（同步）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">同步：提交请求  -&gt;  等待服务器处理  -&gt;  处理完毕返回  （整个期间浏览器不能干任何事）</span>

<span style="color: #008000;">//</span><span style="color: #008000;">异步：请求通过时间触发  -&gt;  服务器处理（这时浏览器可以做做任何事情） -&gt;  处理完毕</span></pre>
</div>
<p>注：open方法不会向服务器发送真正请求，它相当于初始化请求并准备发送，只能向同一个域中使用相同协议和端口的URL发送请求，否则会因为安全原因报错。</p>
<p>&nbsp;</p>
<p><strong>3、设置响应&nbsp; HTTP请求状态变化&nbsp; 的函数</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">onreadystatechange 在 readystatechange 属性发生改变时触发</span>
xmlhttp.onreadystatechange = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
</span><span style="color: #008000;">//</span><span style="color: #008000;">当readyState等于4，表示异步调用成功。</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 0，还用send方法（即没初始化）</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 1，已经用了send方法，正在发生请求</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 2、send方法已经执行完成</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 3、正在 解析响应的内容</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 4、解析响应内容 完成，可以在客户端调用</span>
<span style="color: #0000ff;">if</span>(xmlhttp.readyState === 4<span style="color: #000000;">){

</span><span style="color: #008000;">//</span><span style="color: #008000;">status &gt;= 200 表示异步调用成功</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 100、客户端需要继续发送请求</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 404、表示页面找不到</span><span style="color: #008000;">
//</span><span style="color: #008000;"> ===304、表示近期请求成功过，而且请求内容没有发生改变，还在浏览器缓存中，可以直接使用</span>
<span style="color: #0000ff;">if</span>( (xmlhttp.status &gt;=200 &amp;&amp; xmlhttp.status &lt;300) || xmlhttp.status === 304<span style="color: #000000;">){

</span><span style="color: #008000;">//</span><span style="color: #008000;">异步调用成功后，在这里可以调用那个.php文件的内容</span>

<span style="color: #008000;">//</span><span style="color: #008000;">这里填写第5步的代码（获取异步调用返回的数据）</span>
<span style="color: #000000;">
}
}
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>4、发送HTTP请求</strong></p>
<div class="cnblogs_code">
<pre>send(<span style="color: #0000ff;">null</span>);</pre>
</div>
<p><strong>send(string)&nbsp; &nbsp; &nbsp;&nbsp;</strong>//将请求发送到服务器</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">参数说明：string仅用于post请求

注：仅在post请求时可以传入参数，不需要则发送null，在调用send方法之后，请求被发往服务器</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">在get情况下传递参数，可以在open创建请求时，添加到url地址栏后面（如：./server.php?username=zhangsan&amp;password=123）</span>

<span style="color: #008000;">//</span><span style="color: #008000;">在post情况下传递参数，在send发送请求时，xmlhttp.send( { username:"zhangsan" , password:"123&Prime; } );</span></pre>
</div>
<p>&nbsp;</p>
<p>在post情况下传递参数，必须要设置HTTP头部信息</p>
<p>setRequest(header , value);&nbsp; &nbsp; //设置HTTP头部信息，需要两个参数</p>
<p>xmlhttp.setRequest("Content-type" , "application/x-www-form-urlencoded");&nbsp; &nbsp; //一般我们可以直接写死</p>
<p>&nbsp;</p>
<p><strong>5、获取异步调用返回的数据</strong></p>
<div class="cnblogs_code">
<pre>console.log(xmlhttp.responseText);     <span style="color: #008000;">//</span><span style="color: #008000;">在控制台打印出返回的数据（字符串的形式）</span></pre>
</div>
<p>&nbsp;</p>
<p>//在收到响应后相应数据会填充到xmlhttp对象的属性，有四个相关属性会被填充：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">responseText：从服务器进程返回数据的字符串形式（比较常用）

 responseXML：从服务器进程返回的DOM兼容的文档数据对象

      status：从服务器返回的数字代码，如404(未找到)和200(已就绪)

 status Text：伴随状态吗的字符串信息</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>6、使用Javascript和DOM&nbsp; 实现局部刷新</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> data = JSON.parse(xmlhttp.reponseText);     <span style="color: #008000;">//</span><span style="color: #008000;">第五步代码</span>
<span style="color: #000000;">
xuanren();      </span><span style="color: #008000;">//</span><span style="color: #008000;">第六步代码</span>
 

<span style="color: #0000ff;">function</span> xuanran(){         <span style="color: #008000;">//</span><span style="color: #008000;">这个函数可以放到最外层</span>
<span style="color: #000000;">
$(</span>'p').text(data.xx);     <span style="color: #008000;">//</span><span style="color: #008000;">将p标签的内容换成data的xx属性</span>
<span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>JSON对象的两个方法：</p>
<p><strong>parse()</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">语法：JSON.parse()

功能：用于将JSON字符串转化成对象</span></pre>
</div>
<p><strong>stringify()</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">语法：JSON.stringify()

功能：用于将一个值转为字符串，该字符串应该符合JSON格式，并且可以被JSON.parse()方法还原</span></pre>
</div>
<p><strong>注：JavaScript原生的eval()类似于JSON.parse()方法，可以将json字符串转换为json对象，但是eval()可以执行不符合JSON格式的代码，有可能会包含恶意代码，所以尽量少用</strong></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>JSON</h2>
<h3>什么是JSON？</h3>
<p>JSON(javascript object natation)，全称是JavaScript对象表示法，它是一种数据交换的文本格式，而不是一种编程语言，用于读取结构化数据（2001年Douglas Crockford提出，目的是取代繁琐笨重的XML格式）</p>
<p>&nbsp;</p>
<h3>JSON语法规则</h3>
<p>JSON的语法可以表示以下三种类型的值：</p>
<p><strong>1、简单值：</strong></p>
<p>简单值使用与JavaScript相同的语法，可以在JSON中表示字符串、数值、布尔值和null</p>
<p>字符串必须使用双引号表示，不能使用单引号，数值必须以十进制表示，且不能使用NaN和Infinity</p>
<p>注：JSON不支持JavaScript中的特殊值undefined</p>
<p><strong>2、对象：</strong></p>
<p>对象作为一种复杂数据类型，表示的是一组有序的键值对，而每个键值对中的值可以是简单值，也可以是复杂数据类型的值</p>
<p>JSON中对象的键名必须放在双引号里面，因为JSON不是JavaScript语句，所以没有末尾的分号</p>
<p>注：同一个对象中不能出现两个同名属性</p>
<p><strong>3、数组：</strong></p>
<p>数组也是一种复杂数据类型，表示一组有序的值的列表，可以通过数值索引来访问其中的值</p>
<p>注：数组或对象最后一个成员的后面，不能加逗号</p>
<p>&nbsp;</p>
<h2>jQuery AJAX 方法</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">$.ajax({
url: </span>"", <span style="color: #008000;">//</span><span style="color: #008000;">请求地址</span>
type: "", <span style="color: #008000;">//</span><span style="color: #008000;">请求方式</span>
async: <span style="color: #0000ff;">true</span>, <span style="color: #008000;">//</span><span style="color: #008000;">异步或同步</span>
dataType: "json", <span style="color: #008000;">//</span><span style="color: #008000;">数据格式</span>
success: <span style="color: #0000ff;">function</span>(huidiao) { <span style="color: #008000;">//</span><span style="color: #008000;">请求成功的回调（huidiao表示从服务器返回来的数据）</span>
xuanran(huidiao); <span style="color: #008000;">//</span><span style="color: #008000;">渲染数据</span>
<span style="color: #000000;">}
})

</span><span style="color: #0000ff;">function</span> xuanran(huidiao) { <span style="color: #008000;">//</span><span style="color: #008000;">这个函数可以写到最外层</span><span style="color: #008000;">
//</span><span style="color: #008000;">$.each()可以用来遍历对象</span>
$.each(huidiao, <span style="color: #0000ff;">function</span>(index, obj) { <span style="color: #008000;">//</span><span style="color: #008000;">index表示huidiao里面的每个键，obj表示huidiao里面的每个值</span>
console.log(index + "：" + obj); <span style="color: #008000;">//</span><span style="color: #008000;">打印出每个键值对</span>
<span style="color: #000000;">})
}</span></pre>
</div>
<p>&nbsp;</p>
<p>//JavaScript原生方法也可以进行$.ajax()的封装，如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> $ =<span style="color: #000000;"> {
ajax: </span><span style="color: #0000ff;">function</span><span style="color: #000000;">(options) {
</span><span style="color: #008000;">//</span><span style="color: #008000;">&hellip;</span>
<span style="color: #000000;">}
}</span></pre>
</div>
<p>&nbsp;</p>
<p>$.ajax()</p>
<p>$.get()</p>
<p>$.post()</p>
<p>$.getJson()</p>
<p>&nbsp;</p>
<h2>跨域（js实现）</h2>
<p>同源策略：域名、协议、端口均相同。</p>
<p>&nbsp;</p>
<p>跨域：从一个域名的网页去请求另外一个域名的资源，严格一点的定义就是，非同源策略（域名、协议、端口有一个不相同），就被当作是跨域。</p>
<p>&nbsp;</p>
<p>跨域的实现方法：</p>
<p>1、跨域资源共享（CORS）</p>
<p><strong>2、使用JSONP（常用）</strong></p>
<p>3、修改document.domain</p>
<p>4、使用window.name</p>
<p>&nbsp;</p>
<p>JSONP：JSON with Padding（填充式json）的简写，是应用JSON的一种新方法，也是一种跨域解决方案。</p>
<p>&nbsp;</p>
<p>JSONP由两部分组成：回调函数和数据。</p>
<p>//回调函数是当响应到来时应该在页面中调用的函数</p>
<p>//数据就是传入回调函数中的JSONP数据</p>
<p>如：abc( [{user:1},{id:9}] )&nbsp; &nbsp; &nbsp; //abc表示回调函数，括号里面为json数据</p>
<p>&nbsp;</p>
<p>JSONP原理</p>
<p>//直接用XMLHttpRequest请求不同域上的数据时，是不行的。</p>
<p>//但是在页面上引入不同域上的js脚本文件确是可以的，JSONP就是利用这个特性来实现的。</p>
<p>通过script标签引入js文件&nbsp; <strong>&nbsp;--&gt;</strong>&nbsp; &nbsp;js文件载入成功后&nbsp; <strong>&nbsp;--&gt;</strong>&nbsp; &nbsp;执行我们在url参数中指定的函数</p>
<p>&nbsp;</p>
<h3>跨域封装</h3>
<p>//封装JSONP</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span> getJSONP(url,callback){   <span style="color: #008000;">//</span><span style="color: #008000;">callback为回调函数</span>
<span style="color: #0000ff;">if</span>(!url) <span style="color: #0000ff;">return</span>;         <span style="color: #008000;">//</span><span style="color: #008000;">如果url不存在直接退出</span><span style="color: #008000;">
//</span><span style="color: #008000;">code....</span>
}</pre>
</div>
<p>//发送给服务器的时候，url地址后面必须跟着 回调函数名。如：</p>
<div class="cnblogs_code">
<pre>http:<span style="color: #008000;">//</span><span style="color: #008000;">www.baidu.com?call=abc     //发送给服务器的数据里面为abc，那么回调函数就叫abc</span>

<span style="color: #008000;">//</span><span style="color: #008000;">call可以随意命名，因为目的是把abc填充到call里面，服务器接收到call只会提取里面的abc，而不会在意call叫什么。</span>
<span style="color: #000000;">
http:</span><span style="color: #008000;">//</span><span style="color: #008000;">www.baidu.com?id=6&amp;call=abc     //若url的?后面带有数据，则需要在最后面添加&amp;call=abc</span></pre>
</div>
<p>//服务器返回的时候</p>
<p>abc(&nbsp;[{user:1},{id:9}])&nbsp; &nbsp; &nbsp; //abc为回调函数，里面为json数据</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>//随机生成回调函数名</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">声明数组，用来生成随机函数名</span>
<span style="color: #0000ff;">var</span> a = ['a','b','c','d','e','f','g','h','i','j'<span style="color: #000000;">],
r1 </span>= Math.floor(Math.random()*10<span style="color: #000000;">),
r2 </span>= Math.floor(Math.random()*10<span style="color: #000000;">),
r3 </span>= Math.floor(Math.random()*10<span style="color: #000000;">),
name </span>= a[r1]+a[r2]+<span style="color: #000000;">a[r3],
cbname </span>= 'getJSONP.'+<span style="color: #000000;">name;<br /></span></pre>
</div>
<p>&nbsp;</p>
<p>//把生成的回调函数名，塞到url地址中</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">判断url地址中是否含有?号</span>
<span style="color: #0000ff;">if</span>(url.indexOf('?') === -1<span style="color: #000000;">)
url </span>+= '?jsonp='+<span style="color: #000000;">cbname;
</span><span style="color: #0000ff;">else</span><span style="color: #000000;">
url </span>+= '&amp;jsonp='+<span style="color: #000000;">cbname;<br /></span></pre>
</div>
<p>&nbsp;</p>
<p>//动态创建script标签</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> script = document.createElement('script');</pre>
</div>
<p>//定义script的src属性</p>
<div class="cnblogs_code">
<pre>script.src = url;</pre>
</div>
<p>//把生成的script塞到head里面去</p>
<div class="cnblogs_code">
<pre>document.getElementByTagName("head")[0].appendChild(script);</pre>
</div>
<p>&nbsp;</p>
<p>//定义被脚本执行的回调函数（就是接收服务器返回的数据的函数）</p>
<div class="cnblogs_code">
<pre>getJSONP[name] = <span style="color: #0000ff;">function</span>(data){   <span style="color: #008000;">//</span><span style="color: #008000;">接收的data表示服务器端返回的json数据</span><span style="color: #008000;">
//</span><span style="color: #008000;">当name为变量的时候一定要用方括号，如果用.的话，name就成了死的字符串</span>

<span style="color: #0000ff;">try</span><span style="color: #000000;">{
    callback </span>&amp;&amp;<span style="color: #000000;"> callback(data);    //跨域成功后，如果有回调函数，尝试执行。这个函数就是调用getJSONP的时候 的参数
}</span><span style="color: #0000ff;">catch</span><span style="color: #000000;">(e){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">code...</span>
}<span style="color: #0000ff;">finally</span><span style="color: #000000;">{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">最后删除该函数及script标签</span>
    <span style="color: #0000ff;">delete</span><span style="color: #000000;"> getJSONP[name];
    script.parentNode.removeChild(script);
}

}</span></pre>
</div>
<p>&nbsp;</p>
<p>//合并起来后</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span> getJSONP(url,callback){   <span style="color: #008000;">//</span><span style="color: #008000;">callback为回调函数</span>
<span style="color: #0000ff;">if</span>(!url) <span style="color: #0000ff;">return</span>;         <span style="color: #008000;">//</span><span style="color: #008000;">如果url不存在直接退出</span>

<span style="color: #008000;">//</span><span style="color: #008000;">声明数组，用来生成随机函数名</span>
<span style="color: #0000ff;">var</span> a = ['a','b','c','d','e','f','g','h','i','j'<span style="color: #000000;">],
r1 </span>= Math.floor(Math.random()*10<span style="color: #000000;">),
r2 </span>= Math.floor(Math.random()*10<span style="color: #000000;">),
r3 </span>= Math.floor(Math.random()*10<span style="color: #000000;">),
name </span>= a[r1]+a[r2]+<span style="color: #000000;">a[r3],
cbname </span>= 'getJSONP.'+<span style="color: #000000;">name;

</span><span style="color: #008000;">//</span><span style="color: #008000;">判断url地址中是否含有?号</span>
<span style="color: #0000ff;">if</span>(url.indexOf('?') === -1<span style="color: #000000;">)
url </span>+= '?jsonp='+<span style="color: #000000;">cbname;
</span><span style="color: #0000ff;">else</span><span style="color: #000000;">
url </span>+= '&amp;jsonp='+<span style="color: #000000;">cbname;

</span><span style="color: #008000;">//</span><span style="color: #008000;">动态创建script标签</span>
<span style="color: #0000ff;">var</span> script = document.createElement('script'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">把生成的script塞到head里面去</span>
document.getElementByTagName("head")[0<span style="color: #000000;">].appendChild(script);

</span><span style="color: #008000;">//</span><span style="color: #008000;">定义被脚本执行的回调函数（就是接收服务器返回的数据的函数）</span>
getJSONP[name] = <span style="color: #0000ff;">function</span><span style="color: #000000;">(data){ 
</span><span style="color: #0000ff;">try</span><span style="color: #000000;">{
    callback </span>&amp;&amp; callback(data);    <span style="color: #008000;">//</span><span style="color: #008000;">跨域成功后，如果有回调函数，尝试执行。这个函数就是调用getJSONP的时候 的参数</span>
}<span style="color: #0000ff;">catch</span><span style="color: #000000;">(e){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">code...</span>
}<span style="color: #0000ff;">finally</span><span style="color: #000000;">{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">最后删除该函数及script标签</span>
    <span style="color: #0000ff;">delete</span><span style="color: #000000;"> getJSONP[name];
    script.parentNode.removeChild(script);
}
}

}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>//调用getJSONP</p>
<div class="cnblogs_code">
<pre>getJSONP( "http://www.baidu.com" ,<span style="color: #0000ff;">function</span><span style="color: #000000;">(data){

</span><span style="color: #008000;">//</span><span style="color: #008000;">在访问url地址后（跨域后），要做的事</span><span style="color: #008000;">
//</span><span style="color: #008000;">这个函数就会被getJSONP接收，上面表示为callback</span>
<span style="color: #000000;">
console.log(data);  </span><span style="color: #008000;">//</span><span style="color: #008000;">如果能打印出data表示，跨域成功</span>
<span style="color: #000000;">
});</span></pre>
</div>
<p>&nbsp;</p>
<p>jquery的跨域解决方案</p>
<p>jquery中的$.ajax()是如何实现跨域的？</p>
<p>jquery事如何做到在url后加?callback来实现跨域的？</p>
