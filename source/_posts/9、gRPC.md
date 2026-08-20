---
title: "9、gRPC"
date: "2021-12-05 16:19:00"
tags:
categories:
description: >-
  之前 protobuf 时安装过，不需安装 快速开启 grpc 服务 新建目录 testGrpc 。以及 testGrpc/service 和 testGrpc/client testGrpc 下新建 hello.proto syntax = "proto3"; package tempPackag
---

<p>&nbsp;之前 protobuf 时安装过，不需安装</p>
<p>&nbsp;</p>
<h2>快速开启 grpc 服务</h2>
<p>新建目录 testGrpc 。以及&nbsp;testGrpc/service 和&nbsp;testGrpc/client</p>
<p>&nbsp;</p>
<p>testGrpc 下新建 hello.proto</p>
<div class="cnblogs_code">
<pre>syntax = <span style="color: #800000;">"</span><span style="color: #800000;">proto3</span><span style="color: #800000;">"</span><span style="color: #000000;">;

package tempPackageName;

option go_package </span>= <span style="color: #800000;">"</span><span style="color: #800000;">ginStart/testGrpc/service/helloPackage</span><span style="color: #800000;">"</span>; <span style="color: #008000;">//</span><span style="color: #008000;"> 生成在service文件夹下，包名为 helloPackage

</span><span style="color: #008000;">//</span><span style="color: #008000;"> The greeting service definition.</span>
<span style="color: #000000;">service Greeter {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> Sends a greeting</span>
<span style="color: #000000;">  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> The request message containing the user's name.</span>
<span style="color: #000000;">message HelloRequest {
  </span><span style="color: #0000ff;">string</span> name = <span style="color: #800080;">1</span><span style="color: #000000;">;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> The response message containing the greetings</span>
<span style="color: #000000;">message HelloReply {
  </span><span style="color: #0000ff;">string</span> message = <span style="color: #800080;">1</span><span style="color: #000000;">;
}


</span><span style="color: #008000;">//</span><span style="color: #008000;"> 生成普通结构文件
</span><span style="color: #008000;">//</span><span style="color: #008000;"> protoc --go_out=client --go_opt=paths=source_relative grpc.proto

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 生成 grpc 文件
</span><span style="color: #008000;">//</span><span style="color: #008000;"> protoc --go-grpc_out=service --go-grpc_opt=paths=source_relative grpc.proto </span><span style="color: #008000;">//</span><span style="color: #008000;"> 若是 . 表示当前目录
</span><span style="color: #008000;">//</span><span style="color: #008000;"> --go-grpc_out=service </span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义输出路径
</span><span style="color: #008000;">//</span><span style="color: #008000;"> --go-grpc_opt=paths=source_relative </span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义输入路径
</span><span style="color: #008000;">//</span><span style="color: #008000;"> grpc.proto </span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义需要编译的文件

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 两种文件一起生成
</span><span style="color: #008000;">//</span><span style="color: #008000;"> protoc --go_out=. --go_opt=paths=source_relative \
</span><span style="color: #008000;">//</span><span style="color: #008000;"> --go-grpc_out=. --go-grpc_opt=paths=source_relative \
</span><span style="color: #008000;">//</span><span style="color: #008000;"> grpc.proto</span></pre>
</div>
<p>&nbsp;</p>
<p>执行命令在当前文件夹生成文件</p>
<div class="cnblogs_code">
<pre> protoc --go_out=. --go_opt=paths=<span style="color: #000000;">source_relative \
 </span>--go-grpc_out=. --go-grpc_opt=paths=<span style="color: #000000;">source_relative \
 grpc.proto</span></pre>
</div>
<p>&nbsp;</p>
<p>在 service 下新建 main.go</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">context</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">google.golang.org/grpc</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">log</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">net</span><span style="color: #800000;">"</span><span style="color: #000000;">
    pb </span><span style="color: #800000;">"</span><span style="color: #800000;">project/testGrpc</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 在 hello_grpc.pb.go 里面找到 GreeterServer 接口
</span><span style="color: #008000;">//</span><span style="color: #008000;">type GreeterServer interface {
</span><span style="color: #008000;">//</span>    <span style="color: #008000;">//</span><span style="color: #008000;"> Sends a greeting
</span><span style="color: #008000;">//</span><span style="color: #008000;">    SayHello(context.Context, *HelloRequest) (*HelloReply, error)
</span><span style="color: #008000;">//</span><span style="color: #008000;">    mustEmbedUnimplementedGreeterServer()
</span><span style="color: #008000;">//</span><span style="color: #008000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 根据格式，实现接口

</span><span style="color: #008000;">//</span><span style="color: #008000;"> server is used to implement hello.GreeterServer.</span>
type server <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    pb.UnimplementedGreeterServer
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> SayHello implements hello.GreeterServer</span>
func (s *server) SayHello(ctx context.Context, <span style="color: #0000ff;">in</span> *pb.HelloRequest) (*<span style="color: #000000;">pb.HelloReply, error) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">log.Printf("Received: %v", in.GetName())</span>

    <span style="color: #0000ff;">return</span> &amp;<span style="color: #000000;">pb.HelloReply{
        Message: </span><span style="color: #800000;">"</span><span style="color: #800000;">Hello </span><span style="color: #800000;">"</span> + <span style="color: #0000ff;">in</span><span style="color: #000000;">.GetName(),
    }, nil
}


func main() {

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 监听 tcp 的 50051 端口</span>
    lis, err := net.Listen(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"localhost:50051</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">failed to listen: %v</span><span style="color: #800000;">"</span>, err) <span style="color: #008000;">//</span><span style="color: #008000;"> 监听发生错误就打印出来，随后退出</span>
<span style="color: #000000;">    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 初始化服务</span>
    s :=<span style="color: #000000;"> grpc.NewServer()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册服务</span>
    pb.RegisterGreeterServer(s, &amp;<span style="color: #000000;">server{})

    log.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">server listening at %v</span><span style="color: #800000;">"</span>, lis.Addr()) <span style="color: #008000;">//</span><span style="color: #008000;"> 一些无关紧要的打印信息

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开启服务</span>
    err =<span style="color: #000000;"> s.Serve(lis)

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">failed to serve: %v</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>启动服务端</p>
<div class="cnblogs_code">
<pre>go run service/main.go</pre>
</div>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211204234012357-665272410.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>在 client 下新建main.go</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">context</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">google.golang.org/grpc</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">log</span><span style="color: #800000;">"</span><span style="color: #000000;">
    pb </span><span style="color: #800000;">"</span><span style="color: #800000;">project/testGrpc</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">time</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

func main() {

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开始请求服务端</span>
    conn, err := grpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">localhost:50051</span><span style="color: #800000;">"</span><span style="color: #000000;">, grpc.WithInsecure(), grpc.WithBlock())
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">did not connect: %v</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 请求结束后就自动关闭连接</span>
<span style="color: #000000;">    defer conn.Close()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 初始化客户端连接</span>
    c :=<span style="color: #000000;"> pb.NewGreeterClient(conn)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Contact the server and print out its response.
    </span><span style="color: #008000;">//</span><span style="color: #008000;">name := defaultName
    </span><span style="color: #008000;">//</span><span style="color: #008000;">if len(os.Args) &gt; 1 {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    name = os.Args[1]
    </span><span style="color: #008000;">//</span><span style="color: #008000;">}

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建一个子节点的context,1秒后自动超时</span>
    ctx, cancel :=<span style="color: #000000;"> context.WithTimeout(context.Background(), time.Second)
    defer cancel()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 发送请求体，返回内容</span>
    r, err := c.SayHello(ctx, &amp;pb.HelloRequest{Name: <span style="color: #800000;">"</span><span style="color: #800000;">好家伙</span><span style="color: #800000;">"</span><span style="color: #000000;">})
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">could not greet: %v</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
    }

    log.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Greeting: %s</span><span style="color: #800000;">"</span><span style="color: #000000;">, r.GetMessage())
}</span></pre>
</div>
<p>&nbsp;</p>
<p>客户端开始连接测试</p>
<div class="cnblogs_code">
<pre>go run client/main.go</pre>
</div>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211204233446614-687026950.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>GRPC Gateway 实现</h2>
<p>在主目录新建 hello.yaml</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">type: google.api.Service

config_version: </span><span style="color: #800080;">3</span><span style="color: #000000;">

http:
  rules:
    </span>-<span style="color: #000000;"> selector: tempPackageName.Greeter.SayHello
      </span><span style="color: #0000ff;">get</span>: /haha/{name}</pre>
</div>
<p>&nbsp;</p>
<p>创建 .bat 快捷键 （最后一行是生成gateway）</p>
<div class="cnblogs_code">
<pre>protoc --go_out=. --go_opt=paths=<span style="color: #000000;">source_relative hello.proto
protoc </span>--go-grpc_out=. --go-grpc_opt=paths=<span style="color: #000000;">source_relative  hello.proto
protoc </span>--grpc-gateway_out=. --grpc-gateway_opt=paths=source_relative,grpc_api_configuration=hello.yaml hello.proto</pre>
</div>
<p>&nbsp;</p>
<p>调用生成</p>
<div class="cnblogs_code">
<pre>./gen.bat</pre>
</div>
<p>&nbsp;</p>
<p>在 service/main.go 里面</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">context</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/grpc-ecosystem/grpc-gateway/v2/runtime</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">google.golang.org/grpc</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">log</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">net</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">net/http</span><span style="color: #800000;">"</span><span style="color: #000000;">
    pb </span><span style="color: #800000;">"</span><span style="color: #800000;">project/testGrpc</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

type server </span><span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    pb.UnimplementedGreeterServer
}

func (s </span>*server) SayHello(ctx context.Context, <span style="color: #0000ff;">in</span> *pb.HelloRequest) (*<span style="color: #000000;">pb.HelloReply, error) {

    </span><span style="color: #0000ff;">return</span> &amp;<span style="color: #000000;">pb.HelloReply{
        Message: </span><span style="color: #800000;">"</span><span style="color: #800000;">Hello </span><span style="color: #800000;">"</span>+ <span style="color: #0000ff;">in</span><span style="color: #000000;">.GetName(),
    }, nil
}


func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 新增 grpc gateway</span>
<span style="color: #000000;">    go grpcGateWay()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 监听 tcp 的 8088 端口</span>
    lis, err := net.Listen(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">localhost:50051</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">failed to listen: %v</span><span style="color: #800000;">"</span>, err) <span style="color: #008000;">//</span><span style="color: #008000;"> 监听发生错误就打印出来，随后退出</span>
<span style="color: #000000;">    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 初始化服务</span>
    s :=<span style="color: #000000;"> grpc.NewServer()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册服务</span>
    pb.RegisterGreeterServer(s, &amp;<span style="color: #000000;">server{})

    log.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">server listening at %v</span><span style="color: #800000;">"</span>, lis.Addr()) <span style="color: #008000;">//</span><span style="color: #008000;"> 一些无关紧要的打印信息

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开启服务</span>
    err =<span style="color: #000000;"> s.Serve(lis)

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">failed to serve: %v</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
    }
}

func grpcGateWay() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 生成没有具体内容的上下文</span>
    c :=<span style="color: #000000;"> context.Background()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 给它新增退出功能</span>
    c, cancel :=<span style="color: #000000;"> context.WithCancel(c)
    defer cancel()

    mux :</span>=<span style="color: #000000;"> runtime.NewServeMux()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册 grpc 服务</span>
    err :=<span style="color: #000000;"> pb.RegisterGreeterHandlerFromEndpoint(
        c,
        mux,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">:50051</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        []grpc.DialOption{grpc.WithInsecure()},
    )

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">can not start grpc gateway：%v</span><span style="color: #800000;">"</span><span style="color: #000000;">,err)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 监听端口中的 HTTP 请求，监听到就按照 .yaml 的内容进行分发</span>
    err = http.ListenAndServe(<span style="color: #800000;">"</span><span style="color: #800000;">:8080</span><span style="color: #800000;">"</span><span style="color: #000000;">,mux)

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">can not start grpc gateway：%v</span><span style="color: #800000;">"</span><span style="color: #000000;">,err)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>起服务后，浏览器访问</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211205131246745-1671421273.png" alt="" width="666" height="223" loading="lazy" /></p>
<p>&nbsp;</p>
