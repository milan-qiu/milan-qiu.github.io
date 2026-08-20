---
title: "GRPC 的验证器"
date: "2022-01-08 15:15:00"
tags:
categories:
description: >-
  插件地址 protoc-gen-validate windows下安装 go install github.com/envoyproxy/protoc-gen-validate@latest 保证 @GOPATH/BIN 下有 protoc-gen-validate.exe 保存 validate.
---

<p>插件地址</p>
<p><a href="https://github.com/envoyproxy/protoc-gen-validate" target="_blank">protoc-gen-validate</a></p>
<p>&nbsp;</p>
<p>windows下安装</p>
<p>go install&nbsp;github.com/envoyproxy/protoc-gen-validate@latest</p>
<p>&nbsp;</p>
<p>保证 @GOPATH/BIN 下有 protoc-gen-validate.exe</p>
<p>&nbsp;</p>
<p>保存 <a href="https://github.com/envoyproxy/protoc-gen-validate/blob/main/validate/validate.proto" target="_blank">validate.proto</a> 文件</p>
<p>&nbsp;</p>
<p>简单使用</p>
<div class="cnblogs_code">
<pre>syntax = <span style="color: #800000;">"</span><span style="color: #800000;">proto3</span><span style="color: #800000;">"</span><span style="color: #000000;">;

option go_package</span>=<span style="color: #800000;">"</span><span style="color: #800000;">.;proto</span><span style="color: #800000;">"</span><span style="color: #000000;">;

import </span><span style="color: #800000;">"</span><span style="color: #800000;">validate.proto</span><span style="color: #800000;">"</span><span style="color: #000000;">;

service Greeter {
  rpc SayHello(StreamReqData) returns (StreamResData);
}

message StreamReqData {
  </span><span style="color: #0000ff;">string</span> data = <span style="color: #800080;">1</span> [(validate.rules).<span style="color: #0000ff;">string</span>.len = <span style="color: #800080;">5</span><span style="color: #000000;">];
}

message StreamResData {
  </span><span style="color: #0000ff;">string</span> data = <span style="color: #800080;">1</span> [(validate.rules).<span style="color: #0000ff;">string</span>.len = <span style="color: #800080;">5</span><span style="color: #000000;">];
}</span></pre>
</div>
<p>&nbsp;</p>
<p>生成 *.pb.validate.go</p>
<div class="cnblogs_code">
<pre>protoc --validate_out=<span style="color: #800000;">"</span><span style="color: #800000;">lang=go:.</span><span style="color: #800000;">"</span> stream.proto</pre>
</div>
<p>&nbsp;</p>
<p>可在 server 端拦截器里做参数验证</p>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;"> 拦截器逻辑</span>
    interceptor := func(ctx context.Context, req <span style="color: #0000ff;">interface</span>{}, info *grpc.UnaryServerInfo, handler grpc.UnaryHandler) (resp <span style="color: #0000ff;">interface</span><span style="color: #000000;">{}, err error) {
        
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 验证参数</span>
        p := <span style="color: #0000ff;">new</span><span style="color: #000000;">(proto.StreamReqData)
        err </span>=<span style="color: #000000;"> p.Validate()
        </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
            fmt.Println(err)
        }

        fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">接收到一个请求</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        res,err :</span>=<span style="color: #000000;"> handler(ctx,req)
        fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">请求已完成</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> res,err
    }</span></pre>
</div>
<p>&nbsp;</p>
