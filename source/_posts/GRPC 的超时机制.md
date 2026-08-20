---
title: "GRPC 的超时机制"
date: "2022-01-09 15:13:00"
tags:
categories:
description: >-
  client 端添加超时机制 // 添加超时机制 ctx,_ := context.WithTimeout(context.Background(),time.Second*3) // 执行服务端的方法 res,err := c.SayHello(ctx,&proto.StreamReqData{D
---

<p>client 端添加超时机制</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 添加超时机制</span>
ctx,_ := context.WithTimeout(context.Background(),time.Second*<span style="color: #800080;">3</span><span style="color: #000000;">)

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 执行服务端的方法</span>
res,err := c.SayHello(ctx,&amp;proto.StreamReqData{Data: <span style="color: #800000;">"</span><span style="color: #800000;">hi</span><span style="color: #800000;">"</span>})</pre>
</div>
<p>&nbsp;</p>
<p>超时返回的错误信息为</p>
<div class="cnblogs_code">
<pre>fmt.Println(st.Message()) <span style="color: #008000;">//</span><span style="color: #008000;"> context deadline exceeded</span>
fmt.Println(st.Code()) <span style="color: #008000;">//</span><span style="color: #008000;"> DeadlineExceeded</span></pre>
</div>
<p>&nbsp;</p>
