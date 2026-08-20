---
title: "9、Controller之Response"
date: "2020-06-22 21:23:00"
tags:
categories:
description: >-
  一、将数组转换json数据 // 1、将数组转换json数据 $data = [ 'key1' => 0, 'key2' => 'value2', 'key3' => 'value3' ]; return response()->json($data); 二、重定向 public function
---

<p>一、将数组转换json数据</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 1、将数组转换json数据</span>
$data =<span style="color: #000000;"> [
    </span><span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800080;">0</span><span style="color: #000000;">,
    </span><span style="color: #800000;">'</span><span style="color: #800000;">key2</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">value2</span><span style="color: #800000;">'</span><span style="color: #000000;">,
    </span><span style="color: #800000;">'</span><span style="color: #800000;">key3</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">value3</span><span style="color: #800000;">'</span><span style="color: #000000;">
];
</span><span style="color: #0000ff;">return</span> response()-&gt;json($data);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>二、重定向</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function res(){

</span><span style="color: #008000;">//</span><span style="color: #008000;">2、重定向</span>
<span style="color: #0000ff;">return</span> redirect(<span style="color: #800000;">'</span><span style="color: #800000;">redirect3</span><span style="color: #800000;">'</span>);<span style="color: #008000;">//</span><span style="color: #008000;">重定向到redirect3方法
</span><span style="color: #008000;">//</span><span style="color: #008000;"> return redirect('redirect3')-&gt;with('msg','我是msg的value'); </span><span style="color: #008000;">//</span><span style="color: #008000;">该数据是快闪数据，只发送一次

</span><span style="color: #008000;">//</span><span style="color: #008000;"> return redirect()-&gt;action('XxxController@redirect3'); </span><span style="color: #008000;">//</span><span style="color: #008000;">可以利用action跳转
</span><span style="color: #008000;">//</span><span style="color: #008000;"> return redirect()-&gt;action('XxxController@redirect3')-&gt;with('msg','同样可以发送快闪数据');

</span><span style="color: #008000;">//</span><span style="color: #008000;"> return redirect()-&gt;route('bbc');</span><span style="color: #008000;">//</span><span style="color: #008000;">根据路由别名跳转
</span><span style="color: #008000;">//</span><span style="color: #008000;"> return redirect()-&gt;route('bbc')-&gt;with('msg','路由别名带参数跳转');</span>
<span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>重定向到的页面，接收参数</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function redirect3(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> echo "这里是redirect3的方法";</span>
    echo session(<span style="color: #800000;">'</span><span style="color: #800000;">msg</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">没有接收到数据</span><span style="color: #800000;">'</span>); <span style="color: #008000;">//</span><span style="color: #008000;">用session接收参数</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>三、返回上一页面</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function res(){

</span><span style="color: #008000;">//</span><span style="color: #008000;">3、返回上一个页面</span>
<span style="color: #0000ff;">return</span> redirect()-&gt;<span style="color: #000000;">back();

}</span></pre>
</div>
<p>&nbsp;</p>
