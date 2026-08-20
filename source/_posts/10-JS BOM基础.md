---
title: "10-JS BOM基础"
date: "2020-03-14 09:45:00"
updated: "2020-03-26 14:36:00"
tags:
categories:
description: >-
  window对象方法 定义一个全局变量 var abc = 12 等同与 window.abc = 12 调用一个全局函数 abc() 等同于 window.abc() 弹窗 alert() 等同于 window.alert() confirm() confirm() 等同于 window.conf
---

<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt; font-family: 幼圆;">window对象方法</span></strong></p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-size: 16px;"><strong><span style="font-family: 幼圆;">定义一个全局变量</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> abc = 12 等同与 window.abc = 12</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">调用一个全局函数</span></strong></p>
<div class="cnblogs_code">
<pre>abc()  等同于 window.abc()</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">弹窗</span></strong></p>
<div class="cnblogs_code">
<pre>alert()   等同于   window.alert()</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">confirm()</span></strong></p>
<div class="cnblogs_code">
<pre>confirm()   等同于  window.confirm()      <span style="color: #008000;">//</span><span style="color: #008000;">（对话弹窗）</span>
<span style="color: #000000;">
如：</span>&lt;input id="mm" type="button" value="删除"&gt;

<span style="color: #0000ff;">var</span> mm = document.getElementById("mm"<span style="color: #000000;">);

mm.onclick </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">(){

</span><span style="color: #0000ff;">var</span> result = window.confirm("你确定要删除吗"<span style="color: #000000;">);

</span><span style="color: #0000ff;">if</span>(result)  alert("删除"<span style="color: #000000;">);

</span><span style="color: #0000ff;">else</span>   alert("取消"<span style="color: #000000;">);

}</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>window.prompt</strong></span></p>
<div class="cnblogs_code">
<pre>window.prompt("提示文本","提示框默认文本"<span style="color: #000000;">)；

按确认时，返回值为文本框内容；按取消时，返回值为null</span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>window.open</strong></span></p>
<div class="cnblogs_code">
<pre>window.open("url","name","parameters")  <span style="color: #008000;">//</span><span style="color: #008000;">打开一个新窗口</span>
<span style="color: #000000;">
url：子窗口的url地址

name：给子窗口的名字

parameters：子窗口的各种参数，用逗号隔开

<br />parameters参数：

width = 子窗口宽度  </span>/  height = 子窗口高度  /  left = 子窗口x轴坐标  /<span style="color: #000000;">  top = 子窗口y轴坐标

toolbar = 是否显示浏览器工具栏  </span>/<span style="color: #000000;">  menubar = 是否显示菜单栏   （是：yes或1 ， 不是：no或0）

scrollbars = 是否显示滚动条  </span>/<span style="color: #000000;">  location = 是否显示地址字段

status = 是否添加状态栏</span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>window.close()&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre>window.close()    <span style="color: #008000;">//</span><span style="color: #008000;">关闭当前浏览器窗口</span>
<span style="color: #000000;">
如：btn.onclick </span>= <span style="color: #0000ff;">function</span>(){window.close();}</pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>setTimeout</strong></span></p>
<div class="cnblogs_code">
<pre>setTimeout("alert(123)",2000)      <span style="color: #008000;">//</span><span style="color: #008000;">超时调用。第一个参数可以是函数名/代码串。在2000毫秒后弹出123</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>clearTimeout</strong></span></p>
<div class="cnblogs_code">
<pre>clearTimeout(rew)     <span style="color: #008000;">//</span><span style="color: #008000;">清除超时调用。里面的参数是函数名</span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>setInterval</strong></span></p>
<div class="cnblogs_code">
<pre>setInterval(wer,1000)      <span style="color: #008000;">//</span><span style="color: #008000;">间歇调用。每隔1000毫秒调用一次wer函数</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>clearInterval</strong></span></p>
<div class="cnblogs_code">
<pre>clearInterval(wer)         <span style="color: #008000;">//</span><span style="color: #008000;">清除间歇调用</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 18pt;">location对象属性</span></strong></p>
<p><span style="font-family: 幼圆;">//location 既属于window对象，也属于document对象</span></p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<div class="cnblogs_code">
<pre>location.href      <span style="color: #008000;">//</span><span style="color: #008000;">返回当前页面完整的url地址。等价于window.location.href</span>
<span style="color: #000000;">
location.pathname       </span><span style="color: #008000;">//</span><span style="color: #008000;">返回url中的目录和（或）文件名</span>
<span style="color: #000000;">
 

location.host         </span><span style="color: #008000;">//</span><span style="color: #008000;">返回当前服务器的名称和端口号</span>
<span style="color: #000000;">
location.hostname       </span><span style="color: #008000;">//</span><span style="color: #008000;">返回当前服务器名称</span>
<span style="color: #000000;">
location.host            </span><span style="color: #008000;">//</span><span style="color: #008000;">返回当前服务器的端口号</span>
<span style="color: #000000;">
 

location.hash            </span><span style="color: #008000;">//</span><span style="color: #008000;">返回当前url地址#后面的内容，包括#；如果没有#，则返回空字符串。</span>
<span style="color: #000000;">
location.search        </span><span style="color: #008000;">//</span><span style="color: #008000;">返回当前url地址?后面的内容，包括?；如果没有?，则返回空字符串。</span>
<span style="color: #000000;">
 

location.protocol      </span><span style="color: #008000;">//</span><span style="color: #008000;">返回页面使用的协议</span></pre>
</div>
<h2>&nbsp;</h2>
<h2><span style="font-family: 幼圆;">location对象方法</span></h2>
<p><span style="font-family: 幼圆;"><strong>更改url地址</strong></span></p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){

location.href </span>= "index2.html";      <span style="color: #008000;">//</span><span style="color: #008000;">1秒后跳转到index2页面。有历史记录</span>
<span style="color: #000000;">
window.location </span>= "index2.html";      <span style="color: #008000;">//</span><span style="color: #008000;">1秒后跳转到index2页面。有历史记录</span>

<span style="color: #008000;">//</span><span style="color: #008000;">同样location.hash和location.search也可以更改url地址</span>
<span style="color: #000000;">
location.replace(</span>"index2.html");      <span style="color: #008000;">//</span><span style="color: #008000;">1秒后跳转到index2页面。无历史纪录</span>
<span style="color: #000000;">
},</span>1000)</pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">模仿浏览器后退按钮</span></strong></p>
<div class="cnblogs_code">
<pre>history.back()  或者   history.go(-1)</pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-size: 16px;"><strong><span style="font-family: 幼圆;">模仿浏览器前进按钮</span></strong></span></p>
<div class="cnblogs_code">
<pre>history.forward()   或者   history.go(1<span style="color: #000000;">)

ps：history.go可以前进后后退n步</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 18pt;">screen对象及属性</span></strong></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">获取网页宽高</span></strong></p>
<div class="cnblogs_code">
<pre>获取网页宽高    <span style="color: #008000;">//</span><span style="color: #008000;">固定的。网页最大化，不带工具栏，的宽高</span>
<span style="color: #000000;">
screen.availWidth   </span>/   screen.availHeight</pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">获取网页的宽高</span></strong></p>
<div class="cnblogs_code">
<pre>获取网页的宽高      <span style="color: #008000;">//</span><span style="color: #008000;">会随着宽口浏览器大小的变化而变化</span>
<span style="color: #000000;">
window.innerWidth   </span>/   window.innerHeight</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 18pt;">navigator对象</span></strong></p>
<p><span style="font-family: 幼圆;">userAgent属性：一个只读的字符串，声明了浏览器用于 HTTP 请求的用户代理头的值。</span></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> browser =<span style="color: #000000;"> {
versions: </span><span style="color: #0000ff;">function</span><span style="color: #000000;">() {
</span><span style="color: #0000ff;">var</span> u =<span style="color: #000000;"> navigator.userAgent,
app </span>=<span style="color: #000000;"> navigator.appVersion;
</span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
</span><span style="color: #008000;">//</span><span style="color: #008000;">浏览器版本信息</span>
trident: u.indexOf('Trident') &gt; -1, <span style="color: #008000;">//</span><span style="color: #008000;">IE内核</span>
presto: u.indexOf('Presto') &gt; -1, <span style="color: #008000;">//</span><span style="color: #008000;">opera内核</span>
webKit: u.indexOf('AppleWebKit') &gt; -1, <span style="color: #008000;">//</span><span style="color: #008000;">苹果、谷歌内核</span>
gecko: u.indexOf('Gecko') &gt; -1 &amp;&amp; u.indexOf('KHTML') == -1, <span style="color: #008000;">//</span><span style="color: #008000;">火狐内核</span>
<span style="color: #000000;">
mobile: </span>!!u.match(/AppleWebKit.*Mobile.*/), <span style="color: #008000;">//</span><span style="color: #008000;">是否为移动终端</span>
<span style="color: #000000;">
ios: </span>!!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), <span style="color: #008000;">//</span><span style="color: #008000;">ios终端</span>
android: u.indexOf('Android') &gt; -1 || u.indexOf('Linux') &gt; -1, <span style="color: #008000;">//</span><span style="color: #008000;">android终端或uc浏览器</span>
<span style="color: #000000;">
iPhone: u.indexOf(</span>'iPhone') &gt; -1, <span style="color: #008000;">//</span><span style="color: #008000;">是否为iPhone或者QQHD浏览器</span>
iPad: u.indexOf('iPad') &gt; -1, <span style="color: #008000;">//</span><span style="color: #008000;">是否iPad</span>
webApp: u.indexOf('Safari') == -1 <span style="color: #008000;">//</span><span style="color: #008000;">是否web应用程序，没有头部与底部</span>
<span style="color: #000000;">};
}(),
language: (navigator.browserLanguage </span>||<span style="color: #000000;"> navigator.language).toLowerCase()
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 16px;"><span style="font-family: 幼圆;">&nbsp;</span><span style="font-family: 幼圆;">判断pc端跟移动端</span></span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span> (browser.versions.mobile) console.log('移动设备'<span style="color: #000000;">);
</span><span style="color: #0000ff;">else</span> console.log("PC设备");</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>判断是安卓还是苹果</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span><span style="color: #000000;"> (browser.versions.ios) {
console.log(</span>'IOS系统'<span style="color: #000000;">);
}
</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (browser.versions.android) {
console.log(</span>'Android系统'<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>判断用的是什么浏览器</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span><span style="color: #000000;"> (browser.versions.trident) {
console.log(</span>'IE浏览器'<span style="color: #000000;">);
}
</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (browser.versions.presto) {
console.log(</span>'opera浏览器'<span style="color: #000000;">);
}
</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (browser.versions.webKit) {
console.log(</span>'Safari或Chrome浏览器'<span style="color: #000000;">);
}
</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (browser.versions.gecko) {
console.log(</span>'Firefox浏览器'<span style="color: #000000;">);
}</span></pre>
</div>
