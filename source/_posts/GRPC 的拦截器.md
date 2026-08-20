---
title: "GRPC 的拦截器"
date: "2022-01-03 18:52:00"
updated: "2022-01-03 23:32:00"
tags:
categories:
description: >-
  开源拦截器 go-grpc-middleware 服务端拦截器实现 func main() { // 拦截器逻辑 interceptor := func(ctx context.Context, req interface{}, info *grpc.UnaryServerInfo, handler
---

<p>开源拦截器&nbsp;<a href="https://github.com/grpc-ecosystem/go-grpc-middleware" data-pjax="#repo-content-pjax-container">go-grpc-middleware</a></p>
<p>&nbsp;</p>
<p>服务端拦截器实现</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 拦截器逻辑</span>
    interceptor := func(ctx context.Context, req <span style="color: #0000ff;">interface</span>{}, info *grpc.UnaryServerInfo, handler grpc.UnaryHandler) (resp <span style="color: #0000ff;">interface</span><span style="color: #000000;">{}, err error) {
        fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">接收到一个请求</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        res,err :</span>=<span style="color: #000000;"> handler(ctx,req)
        fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">请求已完成</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> res,err
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 生成拦截器</span>
    opt :=<span style="color: #000000;"> grpc.UnaryInterceptor(interceptor)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 实例化server时，传入拦截器</span>
    s :=<span style="color: #000000;"> grpc.NewServer(opt)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 监听端口</span>
    lis,err := net.Listen(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span><span style="color: #000000;">,PORT)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册服务</span>
    proto.RegisterGreeterServer(s,&amp;<span style="color: #000000;">server{})

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开启服务</span>
    err =<span style="color: #000000;"> s.Serve(lis)

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">failed to serve: %v</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>客户端拦截器实现</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 拦截器逻辑</span>
    interceptor := func(ctx context.Context, method <span style="color: #0000ff;">string</span>, req, reply <span style="color: #0000ff;">interface</span>{}, cc *<span style="color: #000000;">grpc.ClientConn, invoker grpc.UnaryInvoker, opts ...grpc.CallOption) error {
        start :</span>=<span style="color: #000000;"> time.Now()
        err :</span>=<span style="color: #000000;"> invoker(ctx,method,req,reply,cc,opts...)
        fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">耗时%s\n</span><span style="color: #800000;">"</span><span style="color: #000000;">,time.Since(start))
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> err
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 实例化拦截器</span>
    opt :=<span style="color: #000000;"> grpc.WithUnaryInterceptor(interceptor)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 连接前将拦截器传入</span>
    conn,err := grpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">:50053</span><span style="color: #800000;">"</span><span style="color: #000000;">,grpc.WithInsecure(),opt)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    defer conn.Close()


    c :</span>=<span style="color: #000000;"> proto.NewGreeterClient(conn)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 执行服务端的方法</span>
    res,_ := c.SayHello(context.Background(),&amp;proto.StreamReqData{Data: <span style="color: #800000;">"</span><span style="color: #800000;">hi</span><span style="color: #800000;">"</span><span style="color: #000000;">})

    fmt.Println(res)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>client端，通过拦截器添加 metadata</p>
<div class="cnblogs_code">
<pre>type customCredential <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {

}

func (c customCredential) GetRequestMetadata(ctx context.Context, uri ...</span><span style="color: #0000ff;">string</span>) (map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">string</span><span style="color: #000000;">, error) {
    </span><span style="color: #0000ff;">return</span> map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">string</span><span style="color: #000000;">{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">authorization</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">haha</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    },nil
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> RequireTransportSecurity indicates whether the credentials requires
</span><span style="color: #008000;">//</span><span style="color: #008000;"> transport security.</span>
func (c customCredential) RequireTransportSecurity() <span style="color: #0000ff;">bool</span><span style="color: #000000;"> {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">
}

func main() {

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 实例化拦截器</span>
    opt :=<span style="color: #000000;"> grpc.WithPerRPCCredentials(customCredential{})

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 连接前将拦截器传入</span>
    conn,err := grpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">:50053</span><span style="color: #800000;">"</span><span style="color: #000000;">,grpc.WithInsecure(),opt)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    defer conn.Close()


    c :</span>=<span style="color: #000000;"> proto.NewGreeterClient(conn)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 执行服务端的方法</span>
    res,_ := c.SayHello(context.Background(),&amp;proto.StreamReqData{Data: <span style="color: #800000;">"</span><span style="color: #800000;">hi</span><span style="color: #800000;">"</span><span style="color: #000000;">})

    fmt.Println(res)
}</span></pre>
</div>
<p>&nbsp;</p>
