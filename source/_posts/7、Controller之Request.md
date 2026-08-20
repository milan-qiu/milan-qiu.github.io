---
title: "7、Controller之Request"
date: "2020-06-21 18:56:00"
tags:
categories:
description: >-
  一、获取 / 发送 请求前先引入（控制器页） use Illuminate\Http\Request; 二、配置好路由 三、上代码 public function qingqiu(Request $request){ // 1、获取url的某个值 echo $request->input('name
---

<p>一、获取 / 发送 请求前先引入（控制器页）</p>
<div class="cnblogs_code">
<pre>use Illuminate\Http\Request;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>二、配置好路由</p>
<p>&nbsp;</p>
<p>三、上代码</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function qingqiu(Request $request){
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 1、获取url的某个值</span>
    echo $request-&gt;input(<span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span><span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 2、给某个值设置默认，以防获取不到</span>
    echo $request-&gt;input(<span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">zhangzhang</span><span style="color: #800000;">'</span><span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 3、判断url是否存在某值</span>
    <span style="color: #0000ff;">if</span>($request-&gt;has(<span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span><span style="color: #000000;">)){
        echo $request</span>-&gt;input(<span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
        echo </span><span style="color: #800000;">'</span><span style="color: #800000;">那个值不存在</span><span style="color: #800000;">'</span><span style="color: #000000;">;
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 4、获取url的所有参数</span>
    $res = $request-&gt;<span style="color: #000000;">all();
    dd($res);

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 5、输出当前请求的类型</span>
    echo $request-&gt;<span style="color: #000000;">method();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 6、判断当前请求类型是否是xx类型</span>
    <span style="color: #0000ff;">if</span>($request-&gt;isMethod(<span style="color: #800000;">'</span><span style="color: #800000;">POST</span><span style="color: #800000;">'</span><span style="color: #000000;">)){
        echo </span><span style="color: #800000;">'</span><span style="color: #800000;">yes</span><span style="color: #800000;">'</span><span style="color: #000000;">;
    }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
        echo </span><span style="color: #800000;">'</span><span style="color: #800000;">no</span><span style="color: #800000;">'</span><span style="color: #000000;">;
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 判断当前请求类型是否是ajax请求</span>
    $res = $request-&gt;<span style="color: #000000;">ajax();
    dd($res);

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 7、判断当前url是否有Xxx前缀</span>
    $res = $request-&gt;<span style="color: #0000ff;">is</span>(<span style="color: #800000;">'</span><span style="color: #800000;">Xxx/*</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    var_dump($res);

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 8、获取当前url</span>
    $url = $request-&gt;<span style="color: #000000;">url();
    echo $url;
}</span></pre>
</div>
<p>&nbsp;</p>
