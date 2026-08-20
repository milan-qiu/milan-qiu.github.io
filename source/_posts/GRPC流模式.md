---
title: "GRPC流模式"
date: "2022-01-02 18:51:00"
updated: "2022-01-02 18:54:00"
tags:
categories:
description: >-
  简单模式 又称为一元 RPC，类似于常规的 http 请求，客户端发送请求，服务端响应请求 服务端流模式 stream.proto syntax = "proto3"; option go_package=".;proto"; service Greeter { rpc GetStream(Stre
---

<h2>简单模式</h2>
<p>又称为一元 RPC，类似于常规的 http 请求，客户端发送请求，服务端响应请求</p>
<p>&nbsp;</p>
<h2>服务端流模式</h2>
<p>stream.proto</p>
<div class="cnblogs_code">
<pre>syntax = "proto3"<span>;

option go_package=".;proto"<span>;

service Greeter {
  rpc GetStream(StreamReqData) returns (stream StreamResData) {} // 服务端流模式
  rpc PutStream(stream StreamReqData) returns (StreamResData) {} // 客户端流模式
  rpc AllStream(stream StreamReqData) returns (stream StreamResData) {} // 双向流模式
<span>}

message StreamReqData {
  string data = 1<span>;
}

message StreamResData {
  string data = 1<span>;
}

//protoc --go_out=. --go_opt=paths=source_relative \
//--go-grpc_out=. --go-grpc_opt=paths=source_relative \
//stream.proto</span></span></span></span></span></pre>
</div>
<p>&nbsp;</p>
<p>server.go</p>
<div class="cnblogs_code">
<pre>type server <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    proto.UnimplementedGreeterServer
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">GetStream 服务端流模式实现</span>
func (s *server) GetStream(data *<span style="color: #000000;">proto.StreamReqData, streamServer proto.Greeter_GetStreamServer) error {
    </span><span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
        _ </span>= streamServer.Send(&amp;<span style="color: #000000;">proto.StreamResData{
            Data: data.Data</span>+<span style="color: #000000;">strconv.Itoa(i),
        })
        time.Sleep(time.Second </span>* <span style="color: #800080;">2</span><span style="color: #000000;">)
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> nil
}

func main() {
    lis,err :</span>= net.Listen(<span style="color: #800000;">"</span><span style="color: #800000;">tcp</span><span style="color: #800000;">"</span><span style="color: #000000;">,PORT)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    s :</span>=<span style="color: #000000;"> grpc.NewServer()

    proto.RegisterGreeterServer(s,</span>&amp;<span style="color: #000000;">server{})

    err </span>=<span style="color: #000000;"> s.Serve(lis)

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">failed to serve: %v</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>client.go</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    conn,err :</span>= grpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">:50052</span><span style="color: #800000;">"</span><span style="color: #000000;">,grpc.WithInsecure())
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    defer conn.Close()

    c :</span>=<span style="color: #000000;"> proto.NewGreeterClient(conn)
    res,_ :</span>= c.GetStream(context.Background(),&amp;<span style="color: #000000;">proto.StreamReqData{
        Data: </span><span style="color: #800000;">"</span><span style="color: #800000;">看看</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    })

    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> {
        a,err :</span>=<span style="color: #000000;"> res.Recv()
        </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
            panic(err)
        }
        fmt.Println(a)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>客户端流模式</h2>
<p>server.go</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> PutStream 客户端流模式</span>
func (s *<span style="color: #000000;">server) PutStream(streamServer proto.Greeter_PutStreamServer) error {
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;">{
        </span><span style="color: #0000ff;">if</span> a,err := streamServer.Recv(); err !=<span style="color: #000000;"> nil {
            fmt.Println(err.Error())
            </span><span style="color: #0000ff;">break</span><span style="color: #000000;">
        } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
            fmt.Println(a)
        }
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> nil
}</span></pre>
</div>
<p>&nbsp;</p>
<p>client.go</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    conn,err :</span>= grpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">:50052</span><span style="color: #800000;">"</span><span style="color: #000000;">,grpc.WithInsecure())
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    defer conn.Close()

    c :</span>=<span style="color: #000000;"> proto.NewGreeterClient(conn)
    res,_ :</span>=<span style="color: #000000;"> c.PutStream(context.Background())

    </span><span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
        res.Send(</span>&amp;<span style="color: #000000;">proto.StreamReqData{
            Data: </span><span style="color: #800000;">"</span><span style="color: #800000;">我来自客户端</span><span style="color: #800000;">"</span>+<span style="color: #000000;">strconv.Itoa(i),
        })
        time.Sleep(time.Second)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>双向流模式</h2>
<p>serer.go</p>
<div class="cnblogs_code">
<pre>func (s *<span style="color: #000000;">server) AllStream(streamServer proto.Greeter_AllStreamServer) error {
    wg :</span>=<span style="color: #000000;"> sync.WaitGroup{}
    wg.Add(</span><span style="color: #800080;">2</span><span style="color: #000000;">)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 收客户端消息</span>
<span style="color: #000000;">    go func() {
        </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> {
            data,_ :</span>=<span style="color: #000000;"> streamServer.Recv()
            </span><span style="color: #0000ff;">if</span> data !=<span style="color: #000000;"> nil {
                fmt.Println(data.Data)
            }
        }
        wg.Done()
    }()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 发客户端消息</span>
<span style="color: #000000;">    go func() {
        </span><span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
            _ </span>= streamServer.Send(&amp;<span style="color: #000000;">proto.StreamResData{
                Data: </span><span style="color: #800000;">"</span><span style="color: #800000;">我来自服务端</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> strconv.Itoa(i),
            })
            time.Sleep(time.Second)
        }
        wg.Done()
    }()
    wg.Wait()
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> nil
}</span></pre>
</div>
<p>&nbsp;</p>
<p>client.go</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    conn,err :</span>= grpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">:50052</span><span style="color: #800000;">"</span><span style="color: #000000;">,grpc.WithInsecure())
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    defer conn.Close()

    c :</span>=<span style="color: #000000;"> proto.NewGreeterClient(conn)
    res,_ :</span>=<span style="color: #000000;"> c.AllStream(context.Background())

    wg :</span>=<span style="color: #000000;"> sync.WaitGroup{}
    wg.Add(</span><span style="color: #800080;">2</span><span style="color: #000000;">)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 收服务端消息</span>
<span style="color: #000000;">    go func() {
        wg.Done()
        </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> {
            data,_ :</span>=<span style="color: #000000;"> res.Recv()
            </span><span style="color: #0000ff;">if</span> data !=<span style="color: #000000;"> nil {
                fmt.Println(data.Data)
            }
        }
    }()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 发服务端消息</span>
<span style="color: #000000;">    go func() {
        </span><span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
            _ </span>= res.Send(&amp;<span style="color: #000000;">proto.StreamReqData{
                Data: </span><span style="color: #800000;">"</span><span style="color: #800000;">我来自客户端</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> strconv.Itoa(i),
            })
            time.Sleep(time.Second)
        }
        wg.Done()
    }()
    wg.Wait()
}</span></pre>
</div>
<p>&nbsp;</p>
