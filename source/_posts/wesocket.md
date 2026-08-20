---
title: "wesocket"
date: "2022-05-11 23:23:00"
tags:
categories:
description: >-
  websocket包：https://github.com/gorilla/websocket 先从普通http开始 package main import "net/http" func main() { http.HandleFunc("/ws",handleFunc) http.ListenA
---

<p>websocket包：https://github.com/gorilla/websocket</p>
<p>先从普通http开始</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import </span><span style="color: #800000;">"</span><span style="color: #800000;">net/http</span><span style="color: #800000;">"</span><span style="color: #000000;">

func main() {
    http.HandleFunc(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ws</span><span style="color: #800000;">"</span><span style="color: #000000;">,handleFunc)

    http.ListenAndServe(</span><span style="color: #800000;">"</span><span style="color: #800000;">:9090</span><span style="color: #800000;">"</span><span style="color: #000000;">,nil)
}

func handleFunc(w http.ResponseWriter, req </span>*<span style="color: #000000;">http.Request) {
    w.Write([]</span><span style="color: #0000ff;">byte</span>(<span style="color: #800000;">"</span><span style="color: #800000;">hello world</span><span style="color: #800000;">"</span><span style="color: #000000;">))
}</span></pre>
</div>
<p>访问: http://localhost:9090 验证</p>
<p>&nbsp;</p>
<p>升级 websocket&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">log</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">net/http</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">time</span><span style="color: #800000;">"</span>

    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/gorilla/websocket</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

func main() {
    http.HandleFunc(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ws</span><span style="color: #800000;">"</span><span style="color: #000000;">,handleFunc)

    http.ListenAndServe(</span><span style="color: #800000;">"</span><span style="color: #800000;">:9090</span><span style="color: #800000;">"</span><span style="color: #000000;">,nil)
}

func handleFunc(w http.ResponseWriter, req </span>*<span style="color: #000000;">http.Request) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> websocket 一些设置</span>
    u :=<span style="color: #000000;"> websocket.Upgrader{
        CheckOrigin: func(r </span>*http.Request) <span style="color: #0000ff;">bool</span><span style="color: #000000;"> {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span> <span style="color: #008000;">//</span><span style="color: #008000;"> 直接允许非同源</span>
<span style="color: #000000;">        },
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开始升级 ws</span>
    c,err :=<span style="color: #000000;"> u.Upgrade(w, req, nil)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        log.Fatalf(</span><span style="color: #800000;">"</span><span style="color: #800000;">升级ws失败: %v</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
    }
    defer c.Close()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 接收客户端发的数据</span>
<span style="color: #000000;">    go func() {
        </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> {
            m :</span>= make(map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">string</span><span style="color: #000000;">)
            err :</span>= c.ReadJSON(&amp;<span style="color: #000000;">m)
            </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
                fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">读取客户端消息失败: %v\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">
            }
            fmt.Println(m)
        }
    }()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 给客户端返回数据</span>
    <span style="color: #0000ff;">for</span><span style="color: #000000;">{
        err :</span>= c.WriteJSON(map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">string</span><span style="color: #000000;">{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">data</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">haha</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">code</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        })
        </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
            fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">发送给客户端失败: %v\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, err)
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">
        }
        time.Sleep(</span><span style="color: #800080;">3</span> *<span style="color: #000000;"> time.Second)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">w.Write([]byte("hello world"))</span>
}</pre>
</div>
<p>直接用postman验证</p>
<p>&nbsp;</p>
