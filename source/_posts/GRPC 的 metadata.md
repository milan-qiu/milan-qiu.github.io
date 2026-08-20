---
title: "GRPC 的 metadata"
date: "2022-01-03 18:09:00"
tags:
categories:
description: >-
  客户端发送 func main() { conn,err := grpc.Dial(":50052",grpc.WithInsecure()) if err != nil { panic(err) } defer conn.Close() c := proto.NewGreeterClient(co
---

<p>客户端发送</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    conn,err :</span>= grpc.Dial(<span style="color: #800000;">"</span><span style="color: #800000;">:50052</span><span style="color: #800000;">"</span><span style="color: #000000;">,grpc.WithInsecure())
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    defer conn.Close()

    c :</span>=<span style="color: #000000;"> proto.NewGreeterClient(conn)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建metadata

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 第一种方式</span>
    md := metadata.New(map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">string</span><span style="color: #000000;">{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">val1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">key2</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">val2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    })

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 第二种方式</span>
    md =<span style="color: #000000;"> metadata.Pairs(
        </span><span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">val1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">key2</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">val2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        )

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 发送 metadata

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建带有meta的context</span>
    ctx :=<span style="color: #000000;"> metadata.NewOutgoingContext(context.Background(),md)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将 ctx 代替原 context.Background()</span>
    res,_ := c.SayHello(ctx,&amp;proto.StreamReqData{Data: <span style="color: #800000;">"</span><span style="color: #800000;">hi</span><span style="color: #800000;">"</span><span style="color: #000000;">})

    fmt.Println(res)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>服务端获取</p>
<div class="cnblogs_code">
<pre>func (s *server) SayHello (ctx context.Context, <span style="color: #0000ff;">in</span> *proto.StreamReqData) (*<span style="color: #000000;">proto.StreamResData, error) {
    md, _ :</span>=<span style="color: #000000;"> metadata.FromIncomingContext(ctx)
    </span><span style="color: #0000ff;">if</span> md !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 接收所有metadata</span>
<span style="color: #000000;">        fmt.Println(md)
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 循环输出</span>
        <span style="color: #0000ff;">for</span> key,val :=<span style="color: #000000;"> range md {
            fmt.Println(key,val)
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 只取里面的key1</span>
        <span style="color: #0000ff;">if</span> nameSlice,ok := md[<span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span><span style="color: #000000;">]; ok {
            </span><span style="color: #0000ff;">for</span> _,val :=<span style="color: #000000;"> range nameSlice {
                fmt.Println(val)
            }
        }
    }
    </span><span style="color: #0000ff;">return</span> &amp;proto.StreamResData{Data: <span style="color: #800000;">"</span><span style="color: #800000;">你好</span><span style="color: #800000;">"</span><span style="color: #000000;">},nil
}</span></pre>
</div>
<p>&nbsp;</p>
