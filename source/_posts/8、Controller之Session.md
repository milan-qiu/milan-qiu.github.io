---
title: "8、Controller之Session"
date: "2020-06-21 23:03:00"
tags:
categories:
description: >-
  一、session默认配置目录：config / session.php 1、21行，默认使用 file 驱动。还支持"cookie", "database", "apc","memcached", "redis", "dynamodb", "array" 等驱动方式 2、34行，设置session
---

<p>一、session默认配置目录：config / session.php</p>
<p>1、21行，默认使用 file 驱动。还支持"cookie", "database", "apc","memcached", "redis", "dynamodb", "array" 等驱动方式</p>
<p>2、34行，设置session有效期</p>
<p>3、88行，若使用数据库驱动，默认表为sessions</p>
<p>4、laravel中默认开启session start。App / Http / Kernel.php 34行</p>
<p>&nbsp;</p>
<p>二、配置路由，需要用到session的，将其放到中间件里，如：</p>
<div class="cnblogs_code">
<pre>Route::group([<span style="color: #800000;">'</span><span style="color: #800000;">middleware</span><span style="color: #800000;">'</span> =&gt; [<span style="color: #800000;">'</span><span style="color: #800000;">web</span><span style="color: #800000;">'</span><span style="color: #000000;">]] , function(){
    Route::any(</span><span style="color: #800000;">'</span><span style="color: #800000;">/session1</span><span style="color: #800000;">'</span> , <span style="color: #800000;">'</span><span style="color: #800000;">XxxController@session1</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    Route::any(</span><span style="color: #800000;">'</span><span style="color: #800000;">/session2</span><span style="color: #800000;">'</span> , <span style="color: #800000;">'</span><span style="color: #800000;">XxxController@session2</span><span style="color: #800000;">'</span><span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>二、使用session的三种方法</p>
<p>1、Http request类的session方法</p>
<p>先引入</p>
<div class="cnblogs_code">
<pre>use Illuminate\Http\Request;</pre>
</div>
<p>&nbsp;</p>
<p>存取session键值对</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function session1(Request $request){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">存入键值对</span>
    $request-&gt;session()-&gt;put(<span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">value1</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function session2(Request $request){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">读取键值对</span>
    echo $request-&gt;session()-&gt;<span style="color: #0000ff;">get</span>(<span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    echo $request</span>-&gt;session()-&gt;<span style="color: #0000ff;">get</span>(<span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">default</span><span style="color: #800000;">'</span>);<span style="color: #008000;">//</span><span style="color: #008000;">若key1不存在，则用default</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>2、session() 辅助函数</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">session全局辅助函数</span>
<span style="color: #0000ff;">public</span><span style="color: #000000;"> function session1(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">存入键值对</span>
    session([<span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">value</span><span style="color: #800000;">'</span><span style="color: #000000;">]);
}
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function session2(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">读取键值对</span>
    echo session(<span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    echo session(</span><span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">default</span><span style="color: #800000;">'</span>);<span style="color: #008000;">//</span><span style="color: #008000;">若key不存在，则用default</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="text-decoration: line-through;">3、Session facade</span></p>
<p>&nbsp;</p>
<p>三、检索 &amp; 删除一条数据（request方法）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">检索 &amp; 删除一条数据（）</span>
<span style="color: #0000ff;">public</span><span style="color: #000000;"> function session1(Request $request){
    $request</span>-&gt;session()-&gt;put(<span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">value</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function session2(Request $request){
    echo $request</span>-&gt;session()-&gt;pull(<span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">default</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>四、取出session所有的值（request方法）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">取出session所有的值</span>
<span style="color: #0000ff;">public</span><span style="color: #000000;"> function session1(Request $request){
    $request</span>-&gt;session()-&gt;put(<span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">value1</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    $request</span>-&gt;session()-&gt;put(<span style="color: #800000;">'</span><span style="color: #800000;">key2</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">value2</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function session2(Request $request){
    dd($request</span>-&gt;session()-&gt;<span style="color: #000000;">all());
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>五、判断某个值是否<strong>存在，且不为null</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span> ($request-&gt;session()-&gt;has(<span style="color: #800000;">'</span><span style="color: #800000;">users</span><span style="color: #800000;">'</span><span style="color: #000000;">)) {
    </span><span style="color: #008000;">//
</span>}</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>六、判断某个值<strong>是否存在，可以为null</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span> ($request-&gt;session()-&gt;exists(<span style="color: #800000;">'</span><span style="color: #800000;">users</span><span style="color: #800000;">'</span><span style="color: #000000;">)) {
    </span><span style="color: #008000;">//
</span>}</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>七、删除session的值（request方法）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 删除单个值...</span>
$request-&gt;session()-&gt;forget(<span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除多个值...</span>
$request-&gt;session()-&gt;forget([<span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">key2</span><span style="color: #800000;">'</span><span style="color: #000000;">]);

</span><span style="color: #008000;">//</span><span style="color: #008000;">全删</span>
$request-&gt;session()-&gt;flush();</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>八、闪存数据（request方法）</p>
<p>第一次访问存在，第二次访问就消失</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">闪存数据</span>
<span style="color: #0000ff;">public</span><span style="color: #000000;"> function session1(Request $request){
    $request</span>-&gt;session()-&gt;flash(<span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">value</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function session2(Request $request){
    echo $request</span>-&gt;session()-&gt;<span style="color: #0000ff;">get</span>(<span style="color: #800000;">'</span><span style="color: #800000;">key</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
