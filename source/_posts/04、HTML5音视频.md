---
title: "04、HTML5音视频"
date: "2020-03-15 18:27:00"
updated: "2020-04-01 09:29:00"
tags:
categories:
description: >-
  video <video controls> //当video里面省略src时，video里面可以插入多个source，当第一个source的格式不支持时，接着使用第二个source... <source src="xxx.mp4"></source> <source src="xxx.webm">
---

<h2>video</h2>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">video </span><span style="color: #ff0000;">controls</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
//当video里面省略src时，video里面可以插入多个source，当第一个source的格式不支持时，接着使用第二个source... 
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="xxx.mp4"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>   
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="xxx.webm"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="xxx.ogv"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
您的浏览器不支持播放这个视频
//当所有的source都不支持时，显示这句话
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">video</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>src：视频的资源地址</p>
<p>controls：视频播放控件</p>
<p>source：可以放如src，如果播放失败，会继续看下一个source</p>
<p>video标签的支持格式：mp4、webm、ogv（其中ie8及以下不支持video标签，ie9及以上只支持mp4格式）</p>
<p>&nbsp;</p>
<p>width：视频的宽度</p>
<p>height：视频的高度</p>
<p>注：两个一起用的话，vieo盒子生效，视频会按比例缩放到最中间的位置</p>
<p>&nbsp;</p>
<p>autoplay：自动播放（在chrom浏览器中，默认被禁用）</p>
<p>loop：循环播放</p>
<p>&nbsp;</p>
<p>poster：视频封面，没有播放时显示的图片</p>
<p>muted：视频默认静音状态（在chrom浏览器中设置autoplay和muted后，发现autoplay生效了）</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>video API 事件</h2>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #0000ff;">&gt;</span>
<span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">code...</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>play()</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">让视频播放</span>
<span style="color: #0000ff;">var</span> div = document.getElementById('dd'<span style="color: #000000;">);
div.play();</span></pre>
</div>
<p>&nbsp;</p>
<p>pause()</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">让视频暂停</span>
<span style="color: #0000ff;">var</span> div = document.getElementById('dd'<span style="color: #000000;">);
div.pause();</span></pre>
</div>
<p>&nbsp;</p>
<p>duration</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">返回视频的总长度（以秒的形式）。一开始获取不到需要页面都加载完毕之后才能获取到（可以尝试用setTimeout）</span>
setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(div.duration);
},</span>100);<span style="color: #008000;">//</span><span style="color: #008000;">100毫秒后执行</span></pre>
</div>
<p>&nbsp;</p>
<p>currentTime</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">设置/返回当前视频的长度 （以秒为单位）</span>
console.log(div.currentTime);   <span style="color: #008000;">//返回</span><span style="color: #008000;">当前已经播放了的视频长度</span>
div.currentTime = 30;     <span style="color: #008000;">//</span><span style="color: #008000;">把当前的视频长度设置为30秒</span></pre>
</div>
<p>&nbsp;</p>
<p>src</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">设置/返回视频的来源</span>
div.src = "xxx.mp4";   <span style="color: #008000;">//</span><span style="color: #008000;">更改或设置当前视频的src</span>
console.log(div.src);    <span style="color: #008000;">//</span><span style="color: #008000;">返回当前视频的来源</span></pre>
</div>
<p>&nbsp;</p>
<p>volume</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">设置/返回当前的音量大小(0-1)</span>
div.volume = 0.5;   <span style="color: #008000;">//</span><span style="color: #008000;">设置当前音量为一半</span>
console.log(div.volume);   <span style="color: #008000;">//</span><span style="color: #008000;">返回当前的音量大小</span>

<span style="color: #008000;">//</span><span style="color: #008000;">可以尝试用input的range类型来控制</span>
&lt;input type="range" min=0 max=100 value=50 id="range"&gt;
&lt;script type = "text/javascript"&gt;<br /><span style="color: #000000;">div.volume = 0.5;
range.oninput </span>= <span style="color: #0000ff;">function</span>(){  <span style="color: #008000;">//</span><span style="color: #008000;">当触发滑动杆的时候，更改音量</span>
div.volume = <span style="color: #0000ff;">this</span>.value/100;  
<span style="color: #000000;">}
</span>&lt;/script&gt;</pre>
</div>
<p>&nbsp;</p>
<p>controls</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">设置视频是否显示播放控件</span>
div.controls = <span style="color: #0000ff;">true</span>;   <span style="color: #008000;">//</span><span style="color: #008000;">true表示显示控件，false表示隐藏控件</span></pre>
</div>
<p>&nbsp;</p>
<p>muted</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">设置视频是否静音</span>
div.muted = <span style="color: #0000ff;">true</span>;  <span style="color: #008000;">//</span><span style="color: #008000;">true表示静音，false表示非静音</span></pre>
</div>
<p>&nbsp;</p>
<p>networkState</p>
<p>//返回video上面的网络状态</p>
<p>0、未初始化</p>
<p>1、视频已经选区好资源，但是未使用网络</p>
<p>2、浏览器正在下载视频资源</p>
<p>3、未找到视频资源（一开始获取不到需要页面都加载完毕之后才能获取到（可以尝试用setTimeout））</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>currentSrc</p>
<p>//返回音视频的地址（必须是在音视频可以加载播放的时候才能返回，而且不能赋值）</p>
<p>&nbsp;</p>
<p>ended</p>
<p>//返回当前视频是否结束，结束返回true，还没结束返回false</p>
<p>//可以用addEventListener监听事件，当监听到true的是否可以执行函数操作</p>
<p>&nbsp;</p>
<p>loop</p>
<p>//设置或返回当前视频是否循环</p>
<div class="cnblogs_code">
<pre>console.log(videoNode.loop);  <span style="color: #008000;">//</span><span style="color: #008000;">打印出视频是否循环，true/false</span>
videoNode.loop = <span style="color: #0000ff;">false</span>;    <span style="color: #008000;">//</span><span style="color: #008000;">把视频设置为不循环</span></pre>
</div>
<p>&nbsp;</p>
<p>playbackRate</p>
<p>//设置或返回视频的播放速度</p>
<div class="cnblogs_code">
<pre>console.log(videoNode.playbackRate);  <span style="color: #008000;">//</span><span style="color: #008000;">打印出视频的播放速度，默认是1</span>
videoNode.playbackRate = 3;    <span style="color: #008000;">//</span><span style="color: #008000;">把视频设置为3倍速度播放</span></pre>
</div>
<p>&nbsp;</p>
<p>readyState</p>
<p>//返回当前视频的就绪状态</p>
<p>0、没有视频的就绪信息</p>
<p>1、有数据，但是快不足以支撑</p>
<p>2、当前数据是可用的，但是没有数据来播放下一帧</p>
<p>3、数据正在缓冲，当前及下一帧是可用的</p>
<p>4、可用数据足以开始播放</p>
<p>&nbsp;</p>
<p>timeupdate</p>
<p>//但视频播放时，执行函数的内容</p>
<div class="cnblogs_code">
<pre>dd.addEventListener('timeupdate',<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(</span>"视频正在播放"<span style="color: #000000;">);
},false)</span></pre>
</div>
<p>&nbsp;</p>
<p>seeked</p>
<p>//当用户 已经完成 拖动进度条时触发，必须要用on</p>
<div class="cnblogs_code">
<pre>dd.onseeked = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(</span>"seeked...."<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>seeking</p>
<p>//当用户 开始 拖动进度条时触发，必须用on</p>
<div class="cnblogs_code">
<pre>dd.onseeking = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(</span>"seeking...."<span style="color: #000000;">);
}<br />//实践证明seeking的触发频率比seeked高</span></pre>
</div>
<p>&nbsp;</p>
<p>volumechange</p>
<p>//当音量已更改时触发，必须用on</p>
<div class="cnblogs_code">
<pre>dd.onvolumechange = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(</span>"声音已发生改变"<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>RequestFullScreen</p>
<p>//全屏，必须在用户的事件中调用，且谷歌内核(webkit)、火狐内核(moz)、IE内核(ms)&nbsp; 的方法都不一样</p>
<div class="cnblogs_code">
<pre>&lt;input type="button" id="full" vallue="全屏" /&gt;
<span style="color: #0000ff;">var</span> full = document.getElementById('full'<span style="color: #000000;">);<br />
full.onclick </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
</span><span style="color: #0000ff;">if</span>(dd.webkitRequestFullscreen)  <span style="color: #008000;">//</span><span style="color: #008000;">webkit内核</span>
<span style="color: #000000;">dd.webkitRequestFullscreen();
</span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span>(dd.mozReuestFullScreen)  <span style="color: #008000;">//</span><span style="color: #008000;">moz内核</span>
<span style="color: #000000;">dd.mozRequestFullScreen();
</span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span>()  <span style="color: #008000;">//</span><span style="color: #008000;">IE内核</span><span style="color: #008000;">
//</span><span style="color: #008000;">code....</span>
}<br />//如果视频没有加controls，想要退出全屏时，会自动加上controls</pre>
</div>
<p>&nbsp;</p>
<p>load</p>
<p>//重新加载视频资源</p>
<div class="cnblogs_code">
<pre>&lt;input type="button" id="shuaxin" value = "刷新视频" /&gt;
<span style="color: #0000ff;">var</span> shuaxin = document.getElementById('shuaxin'<span style="color: #000000;">);

shuaxin.onclick </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
dd.load();
}</span></pre>
</div>
<p>&nbsp;</p>
<p>canplay</p>
<p>//视频已经加载好，可以播放时的事件</p>
<div class="cnblogs_code">
<pre>dd.addEventListener('canplay',<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(</span>"视频已经加载好，可以正常播放"<span style="color: #000000;">);
})</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>audio</h2>
<div class="cnblogs_code">
<pre>&lt;audio controls&gt;<span>
//当audio里面省略src时，audio里面可以插入多个source，当第一个source的格式不支持时，接着使用第二个source... 
&lt;source src="xxx.mp3"&gt;&lt;/source&gt;   
&lt;source src="xxx.wav"&gt;&lt;/source&gt;
&lt;source src="xxx.ogg"&gt;&lt;/source&gt;<span>
您的浏览器不支持播放这个音频
//当所有的source都不支持时，显示这句话
&lt;/audio&gt;</span></span></pre>
</div>
<p>src：音频的资源地址</p>
<p>controls：音频播放控件</p>
<p>source：可以放如src，如果播放失败，会继续看下一个source</p>
<p>&nbsp;</p>
<p>audio标签的支持格式：mp3、wav、ogg（其中ie8及以下不支持audio标签，ie9及以上只支持mp3格式）</p>
<p>mp3（所有浏览器都支持）</p>
<p>wav（所有浏览器都支持）</p>
<p>ogg（safari不支持）</p>
<p>&nbsp;</p>
<p>如果HTML没有audio标签，JavaScript可以生成如：</p>
<p>console.log(new Audio(););&nbsp; //生成&lt;audio&gt;&lt;/audio&gt;</p>
<p>&nbsp;</p>
<p>autoplay</p>
<p>//chrome、opera浏览器不能自动播放音频，需要进行页面元素交互才能播放</p>
<p>&nbsp;</p>
<p>muted</p>
<p>//静音属性</p>
<p>//就算有了这个属性，audio也不会自动播放</p>
<p>&nbsp;</p>
<p>loop</p>
<p>//音频循环播放</p>
<p>&nbsp;</p>
<p>注：audio不能直接在html里面添加width，需要在css中控制audio的width才能起作用。height也是，不过height只能起到占位的效果</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>audio API事件</h2>
<p>跟video一样</p>
<div class="cnblogs_code">
<pre>       play：当音频播放/不在暂停时
      pause：当音频已经暂停时/不在播放时
<span style="color: #000000;">   duration：返回当前音频长度
currentTime：设置或返回当前音频的长度
        src：设置</span>/返回当前音频的来源
     volume：设置/返回当前音频的音量
<span style="color: #000000;">   controls：设置音频是否显示控件
      muted：设置音频是否静音
networkState：返回音频的当前网络状态<br /><br /></span></pre>
<p>&nbsp; currentSrc：返回当前音频的url，不能更改<br />&nbsp; &nbsp; &nbsp; &nbsp;ended：返回音频的播放是否已结束<br />&nbsp; &nbsp; &nbsp; &nbsp; loop：设置或返回音频是否循环<br />playbackRate：设置或返回音频播放的速度<br />&nbsp; readyState：属性返回音频的当前就绪状态<br />&nbsp; timeupdate：当目前的音频位置已更改时<br />&nbsp; &nbsp; &nbsp; seeked：当用户已移动/跳跃到视频中新的位置时<br />&nbsp; &nbsp; &nbsp;seeking：当用户开始移动/跳跃到音频的新位置时<br />volumechange：当音量已更改时</p>
<p>&nbsp;</p>
<p>load：重新加载音频资源</p>
<p>canplay：音频已准备好，可以开始播放</p>
</div>
<p>&nbsp;</p>
<p>requestFulScreen：全屏</p>
<p>//用js创建的audio不能控制它全屏，只有在html创建的audio才行</p>
<p>&nbsp;</p>
