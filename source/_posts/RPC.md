---
title: "RPC"
date: "2022-01-02 14:41:00"
tags:
categories:
description: >-
  1、RPC (Remote Procedure Call) 远程过程调用 （一个节点请求另一个节点提供的服务） 2、对应 RPC 的是本地过程调用，函数调用是最常见的本地过程调用 3、将本地过程调用，变成远程过程调用会面临各种问题 go 内置简单 rpc 调用 server 端 package ma
---

<p>1、RPC (Remote Procedure Call) 远程过程调用 （一个节点请求另一个节点提供的服务）</p>
<p>&nbsp;</p>
<p>2、对应 RPC 的是本地过程调用，函数调用是最常见的本地过程调用</p>
<p>&nbsp;</p>
<p>3、将本地过程调用，变成远程过程调用会面临各种问题</p>
<p>&nbsp;</p>
<h3>go 内置简单 rpc 调用</h3>
<p>server 端</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">net</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">net/rpc</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

type HelleService </span><span style="color: #0000ff;">struct</span><span style="color: #000000;"> {

}

func (s </span>* HelleService) Hello (request <span style="color: #0000ff;">string</span>, reply * <span style="color: #0000ff;">string</span><span style="color: #000000;">) error {
    </span>*reply = <span style="color: #800000;">"</span><span style="color: #800000;">hello</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> request
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> nil
}

func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 实例化一个 server</span>
    listener, _ := net.Listen(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">:1234</span><span style="color: #800000;">"</span><span style="color: #000000;">)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册处理逻辑 handler</span>
    _ = rpc.RegisterName(<span style="color: #800000;">"</span><span style="color: #800000;">HelloService</span><span style="color: #800000;">"</span>, &amp;<span style="color: #000000;">HelleService{})

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 启动服务</span>
    conn,_ :=<span style="color: #000000;"> listener.Accept()
    rpc.ServeConn(conn)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>client 端</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">net/rpc</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 建立连接</span>
    client, err := rpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">localhost:1234</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">连接错误</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    </span><span style="color: #0000ff;">var</span> reply <span style="color: #0000ff;">string</span><span style="color: #000000;">
    err </span>= client.Call(<span style="color: #800000;">"</span><span style="color: #800000;">HelloService.Hello</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">liang</span><span style="color: #800000;">"</span>, &amp;<span style="color: #000000;">reply)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">调用失败</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    fmt.Println(reply)
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>替换 rpc 的序列化协议为 json （原 Gob）</h3>
<p>server 端</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 实例化一个 server</span>
    listener, _ := net.Listen(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">:1234</span><span style="color: #800000;">"</span><span style="color: #000000;">)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册处理逻辑 handler</span>
    _ = rpc.RegisterName(<span style="color: #800000;">"</span><span style="color: #800000;">HelloService</span><span style="color: #800000;">"</span>, &amp;<span style="color: #000000;">HelleService{})

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 启动服务</span>
    <span style="color: #0000ff;">for</span><span style="color: #000000;"> {
        conn,_ :</span>=<span style="color: #000000;"> listener.Accept()
        go rpc.ServeCodec(jsonrpc.NewServerCodec(conn))        
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>client 端</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 建立连接</span>
    conn, err := net.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">localhost:1234</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">连接错误</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    </span><span style="color: #0000ff;">var</span> reply <span style="color: #0000ff;">string</span><span style="color: #000000;">
    client :</span>=<span style="color: #000000;"> rpc.NewClientWithCodec(jsonrpc.NewClientCodec(conn))
    err </span>= client.Call(<span style="color: #800000;">"</span><span style="color: #800000;">HelloService.Hello</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">liang</span><span style="color: #800000;">"</span>, &amp;<span style="color: #000000;">reply)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">调用失败</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    fmt.Println(reply)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>任何语言都能进行 rpc 访问，如python</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211223204403114-736141569.png" alt="" width="502" height="351" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>替换 rpc 传输协议为 http （原 tcp）</h3>
<p>server 端</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 实例化一个 server</span>
    _ = rpc.RegisterName(<span style="color: #800000;">"</span><span style="color: #800000;">HelloService</span><span style="color: #800000;">"</span>, &amp;<span style="color: #000000;">HelleService{})
    http.HandleFunc(</span><span style="color: #800000;">"</span><span style="color: #800000;">/wahaha</span><span style="color: #800000;">"</span>,func(w http.ResponseWriter, r *<span style="color: #000000;">http.Request) {
        </span><span style="color: #0000ff;">var</span> conn io.ReadWriteCloser = <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
            io.Writer
            io.ReadCloser
        }{
            ReadCloser: r.Body,
            Writer: w,
        }
        rpc.ServeRequest(jsonrpc.NewServerCodec(conn))
    })

    http.ListenAndServe(</span><span style="color: #800000;">"</span><span style="color: #800000;">:1234</span><span style="color: #800000;">"</span><span style="color: #000000;">,nil)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>测试</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211223210344911-328621120.png" alt="" width="621" height="348" loading="lazy" /></p>
<p>&nbsp;</p>
