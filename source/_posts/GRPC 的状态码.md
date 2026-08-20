---
title: "GRPC 的状态码"
date: "2022-01-08 16:15:00"
tags:
categories:
description: >-
  官方文档 https://github.com/grpc/grpc/blob/master/doc/statuscodes.md 使用时引入 import ( "google.golang.org/grpc/codes" "google.golang.org/grpc/status" ) serve
---

<p>官方文档&nbsp;<a href="https://github.com/grpc/grpc/blob/master/doc/statuscodes.md" target="_blank">https://github.com/grpc/grpc/blob/master/doc/statuscodes.md</a></p>
<div>
<div>&nbsp;</div>
<div>使用时引入
<div class="cnblogs_code">
<pre><span style="color: #000000;">import (
</span><span style="color: #800000;">"</span><span style="color: #800000;">google.golang.org/grpc/codes</span><span style="color: #800000;">"</span>
<span style="color: #800000;">"</span><span style="color: #800000;">google.golang.org/grpc/status</span><span style="color: #800000;">"</span><span style="color: #000000;">
)</span></pre>
</div>
<p>&nbsp;</p>
</div>
</div>
<p>server 端返回错误</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 验证参数</span>
p := <span style="color: #0000ff;">new</span><span style="color: #000000;">(proto.StreamReqData)
err </span>=<span style="color: #000000;"> p.Validate()
</span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
    </span><span style="color: #0000ff;">return</span> nil, status.Error(codes.InvalidArgument,<span style="color: #800000;">"</span><span style="color: #800000;">无效参数</span><span style="color: #800000;">"</span><span style="color: #000000;">)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>client 端可以解析错误</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 执行服务端的方法</span>
res,err := c.SayHello(context.Background(),&amp;proto.StreamReqData{Data: <span style="color: #800000;">"</span><span style="color: #800000;">hi</span><span style="color: #800000;">"</span><span style="color: #000000;">})

</span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
    st,ok :</span>=<span style="color: #000000;"> status.FromError(err)
    </span><span style="color: #0000ff;">if</span> !<span style="color: #000000;">ok {
        fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">不是grpc定义的错误码，无法解析</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }
    fmt.Println(st.Message()) </span><span style="color: #008000;">//</span><span style="color: #008000;"> 无效参数</span>
    fmt.Println(st.Code()) <span style="color: #008000;">//</span><span style="color: #008000;"> InvalidArgument</span>
}<br />fmt.Println(res)</pre>
</div>
<p>&nbsp;</p>
