---
title: "2、rocketmq 简单使用"
date: "2022-02-22 15:09:00"
tags:
categories:
description: >-
  使用 rocketmq-client-go 调用 官方How to use 发送普通消息 package main import ( "context" "fmt" "github.com/apache/rocketmq-client-go/v2" "github.com/apache/rocket
---

<p>使用 <a href="https://github.com/apache/rocketmq-client-go" target="_blank">rocketmq-client-go</a>&nbsp;调用</p>
<p>官方<a href="https://github.com/apache/rocketmq-client-go/blob/master/docs/Introduction.md" target="_blank">How to use</a></p>
<p>&nbsp;</p>
<h2>发送普通消息</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">context</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/apache/rocketmq-client-go/v2</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/apache/rocketmq-client-go/v2/primitive</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/apache/rocketmq-client-go/v2/producer</span><span style="color: #800000;">"</span><span style="color: #000000;">
)
func main() {
    p,err :</span>= rocketmq.NewProducer(producer.WithNameServer([]<span style="color: #0000ff;">string</span>{<span style="color: #800000;">"</span><span style="color: #800000;">172.31.224.1:9876</span><span style="color: #800000;">"</span><span style="color: #000000;">}))
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">produce 生成失败</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    </span><span style="color: #0000ff;">if</span> err = p.Start(); err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">produce 启动失败</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    res,err :</span>= p.SendSync(context.Background(),primitive.NewMessage(<span style="color: #800000;">"</span><span style="color: #800000;">hellomq</span><span style="color: #800000;">"</span>,[]<span style="color: #0000ff;">byte</span>(<span style="color: #800000;">"</span><span style="color: #800000;">hello i m message</span><span style="color: #800000;">"</span><span style="color: #000000;">)))
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">发送失败</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">发送成功</span><span style="color: #800000;">"</span><span style="color: #000000;">,res.String())

    </span><span style="color: #0000ff;">if</span> err = p.Shutdown(); err !=<span style="color: #000000;"> nil {
        panic(</span><span style="color: #800000;">"</span><span style="color: #800000;">关闭 produce 失败</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>消费消息</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    c,_ :</span>=<span style="color: #000000;"> rocketmq.NewPushConsumer(
        consumer.WithNameServer([]</span><span style="color: #0000ff;">string</span>{<span style="color: #800000;">"</span><span style="color: #800000;">172.31.224.1:9876</span><span style="color: #800000;">"</span><span style="color: #000000;">}),
        consumer.WithGroupName(</span><span style="color: #800000;">"</span><span style="color: #800000;">imgroup</span><span style="color: #800000;">"</span>), <span style="color: #008000;">//</span><span style="color: #008000;"> groupname 用于负载均衡，某个消息被这个主机消费了，别的主机就不会去消费</span>
<span style="color: #000000;">    )

    _ </span>= c.Subscribe(<span style="color: #800000;">"</span><span style="color: #800000;">hellomq</span><span style="color: #800000;">"</span>,consumer.MessageSelector{}, func(ctx context.Context, ext ...*<span style="color: #000000;">primitive.MessageExt) (consumer.ConsumeResult, error) {
        </span><span style="color: #0000ff;">for</span> i :=<span style="color: #000000;"> range ext{
            fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">获取到值</span><span style="color: #800000;">"</span><span style="color: #000000;">,ext[i])
        }
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> consumer.ConsumeSuccess,nil
    })

    _ </span>=<span style="color: #000000;"> c.Start()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 不能让 主 routine 退出</span>
<span style="color: #000000;">    time.Sleep(time.Hour)

    _ </span>=<span style="color: #000000;"> c.Shutdown()
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>延迟消息</h2>
<p>多数用来做库存归还</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    p,_ :</span>= rocketmq.NewProducer(producer.WithNameServer([]<span style="color: #0000ff;">string</span>{<span style="color: #800000;">"</span><span style="color: #800000;">172.31.224.1:9876</span><span style="color: #800000;">"</span><span style="color: #000000;">}))

    _ </span>=<span style="color: #000000;"> p.Start()

    msg :</span>= primitive.NewMessage(<span style="color: #800000;">"</span><span style="color: #800000;">hellomq</span><span style="color: #800000;">"</span>,[]<span style="color: #0000ff;">byte</span>(<span style="color: #800000;">"</span><span style="color: #800000;">i m delay message</span><span style="color: #800000;">"</span><span style="color: #000000;">))

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 级别 1s 5s 10s 30s 1m 2m 3m 4m 5m 6m 7m 8m 9m 10m 20m 30m 1h 2h</span>
    msg.WithDelayTimeLevel(<span style="color: #800080;">3</span>) <span style="color: #008000;">//</span><span style="color: #008000;"> 3是10s</span>
<span style="color: #000000;">
    res,_ :</span>=<span style="color: #000000;"> p.SendSync(context.Background(),msg)

    fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">发送成功</span><span style="color: #800000;">"</span><span style="color: #000000;">,res.String())

    _ </span>=<span style="color: #000000;"> p.Shutdown()
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>事务消息</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">context</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/apache/rocketmq-client-go/v2</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/apache/rocketmq-client-go/v2/primitive</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/apache/rocketmq-client-go/v2/producer</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">time</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

type Orderlistener </span><span style="color: #0000ff;">struct</span><span style="color: #000000;">{}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 事务开始</span>
func (*Orderlistener) ExecuteLocalTransaction(msg *<span style="color: #000000;">primitive.Message) primitive.LocalTransactionState {
    fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始执行一些逻辑</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    time.Sleep(time.Second </span>* <span style="color: #800080;">5</span><span style="color: #000000;">)
    fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">逻辑执行结束</span><span style="color: #800000;">"</span><span style="color: #000000;">)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 若是成功就进行投递
    </span><span style="color: #008000;">//</span><span style="color: #008000;">return primitive.CommitMessageState

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 失败直接进行回滚
    </span><span style="color: #008000;">//</span><span style="color: #008000;">return primitive.RollbackMessageState

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 长时间无响应就标记 UnknowState 进行消息回查</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> primitive.UnknowState
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 消息回查（当服务宕掉，下次进去还会进行回查）</span>
func (*Orderlistener) CheckLocalTransaction(msg *<span style="color: #000000;">primitive.MessageExt) primitive.LocalTransactionState {

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开始进行回查</span>
    fmt.Println(<span style="color: #800000;">"</span><span style="color: #800000;">开始进行回查</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    time.Sleep(time.Second </span>* <span style="color: #800080;">5</span><span style="color: #000000;">)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 回查成功就投递，失败就回滚</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> primitive.CommitMessageState
    </span><span style="color: #008000;">//</span><span style="color: #008000;">return primitive.RollbackMessageState</span>
<span style="color: #000000;">}

func main() {
    p,_ :</span>= rocketmq.NewTransactionProducer(&amp;Orderlistener{},producer.WithNameServer([]<span style="color: #0000ff;">string</span>{<span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.163:9876</span><span style="color: #800000;">"</span><span style="color: #000000;">}))

    _ </span>=<span style="color: #000000;"> p.Start()

    res,err :</span>= p.SendMessageInTransaction(context.Background(),primitive.NewMessage(<span style="color: #800000;">"</span><span style="color: #800000;">hellomq</span><span style="color: #800000;">"</span>,[]<span style="color: #0000ff;">byte</span>(<span style="color: #800000;">"</span><span style="color: #800000;">i am transaction mq rollback</span><span style="color: #800000;">"</span><span style="color: #000000;">)))

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">发送成功</span><span style="color: #800000;">"</span><span style="color: #000000;">,res.String())

    time.Sleep(time.Hour)

    _ </span>=<span style="color: #000000;"> p.Shutdown()
}</span></pre>
</div>
<p>&nbsp;</p>
