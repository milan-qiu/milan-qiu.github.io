---
title: "1、elasticseatch 创建数据"
date: "2022-02-18 21:32:00"
tags:
categories:
description: >-
  查看所有 index GET _cat/indices 查看某个 index 基本信息 GET /user put 创建 / 更新 index PUT account/_doc/1 { "name":"明明", "age":18, "companies":[ { "name":"one", "add
---

<p>查看所有 index</p>
<div class="cnblogs_code">
<pre>GET _cat/indices</pre>
</div>
<p>&nbsp;</p>
<p>查看某个 index 基本信息</p>
<div class="cnblogs_code">
<pre>GET /user</pre>
</div>
<p>&nbsp;</p>
<p>put 创建 / 更新 index</p>
<div class="cnblogs_code">
<pre>PUT account/_doc/<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">明明</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">18</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">companies</span><span style="color: #800000;">"</span><span style="color: #000000;">:[
  {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">one</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">address</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">beijing</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }  
  ]
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 若id不存在就创建 account，指定id为1
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 若id存在就更新 account<br />// PUT 方法必须传id</span></pre>
</div>
<p>&nbsp;</p>
<p>post 创建 / 更新数据</p>
<div class="cnblogs_code">
<pre>POST user/_doc/<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 传id时，用法与put一致</span>
<span style="color: #000000;">
POST user</span>/_doc/<span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800080;">2</span><span style="color: #000000;">
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 不传id时，表示新增</span></pre>
</div>
<p>&nbsp;</p>
<p>post + _create 数据不存在就创建，存在就报错</p>
<div class="cnblogs_code">
<pre>POST user/_create/<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
