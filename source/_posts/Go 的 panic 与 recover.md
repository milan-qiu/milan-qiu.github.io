---
title: "Go 的 panic 与 recover"
date: "2022-03-02 08:50:00"
tags:
categories:
description: >-
  简单使用 func main() { fmt.Println("c") defer func() { // 必须要先声明defer，否则不能捕获到panic异常 fmt.Println("d") if err := recover(); err != nil { fmt.Println(err) /
---

<p>简单使用</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
      fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">c</span><span style="color: #800000;">"</span><span style="color: #000000;">)
   defer func() { </span><span style="color: #008000;">//</span><span style="color: #008000;"> 必须要先声明defer，否则不能捕获到panic异常</span>
      fmt.Println(<span style="color: #800000;">"</span><span style="color: #800000;">d</span><span style="color: #800000;">"</span><span style="color: #000000;">)
      </span><span style="color: #0000ff;">if</span> err := recover(); err !=<span style="color: #000000;"> nil {
         fmt.Println(err) </span><span style="color: #008000;">//</span><span style="color: #008000;"> 这里的err其实就是panic传入的内容</span>
<span style="color: #000000;">      }
      fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">e</span><span style="color: #800000;">"</span><span style="color: #000000;">)
   }()
   f() </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调用f</span>
   fmt.Println(<span style="color: #800000;">"</span><span style="color: #800000;">f</span><span style="color: #800000;">"</span>) <span style="color: #008000;">//</span><span style="color: #008000;">这里开始下面代码不会再执行</span>
<span style="color: #000000;">}

func f() {
   fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">)
   panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">异常信息</span><span style="color: #800000;">"</span><span style="color: #000000;">)
   fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">b</span><span style="color: #800000;">"</span>) <span style="color: #008000;">//</span><span style="color: #008000;">这里开始下面代码不会再执行</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>-------output-------<br />c<br />a<br />d<br />异常信息<br />e</p>
<p>&nbsp;</p>
<p>转自：<a href="https://www.jianshu.com/p/0cbc97bd33fb" target="_blank">https://www.jianshu.com/p/0cbc97bd33fb</a></p>
