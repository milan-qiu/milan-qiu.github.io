---
title: "sentinel 限流、熔断、降级"
date: "2022-05-11 23:29:00"
updated: "2023-01-03 13:11:00"
tags:
categories:
description: >-
  限流：为了用户体验，当流量超过了服务自身范围，拒绝超出的流量访问 熔断：系统在设计之初就把熔断措施考虑进去。当系统出现问题时，如果短时间内无法修复，系统要自动做出判断，开启熔断开关，拒绝流量访问，避免大流量对后端的过载请求。 降级：将系统的所有功能服务进行一个分级，当系统出现问题需要紧急限流时，可将
---

<p>限流：为了用户体验，当流量超过了服务自身范围，拒绝超出的流量访问</p>
<p>熔断：<span class="lake-fontsize-14" data-spm-anchor-id="a2c6h.12873639.article-detail.i2.5ae464a39KEOh8">系统在设计之初就把熔断措施考虑进去。当系统出现问题时，如果短时间内无法修复，系统要自动做出判断，开启熔断开关，拒绝流量访问，避免大流量对后端的过载请求。</span></p>
<p>降级：<span class="lake-fontsize-14" data-spm-anchor-id="a2c6h.12873639.article-detail.i4.5ae464a39KEOh8">将系统的所有功能服务进行一个分级，当系统出现问题需要紧急限流时，可将不是那么重要的功能进行降级处理，停止服务，这样可以释放出更多的资源供给核心功能的去用。</span></p>
<p><a href="https://github.com/alibaba/sentinel-golang" target="_blank">官方文档</a></p>
<p>&nbsp;example</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span><span style="color: #000000;">
    sentinel </span><span style="color: #800000;">"</span><span style="color: #800000;">github.com/alibaba/sentinel-golang/api</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/alibaba/sentinel-golang/core/base</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/alibaba/sentinel-golang/core/flow</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 初始化 sentinel</span>
    err :=<span style="color: #000000;"> sentinel.InitDefault()
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 配置限流规则</span>
    _,err = flow.LoadRules([]*<span style="color: #000000;">flow.Rule{
        {
            Resource:               </span><span style="color: #800000;">"</span><span style="color: #800000;">some-test</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Threshold:              </span><span style="color: #800080;">10</span>, <span style="color: #008000;">//</span><span style="color: #008000;"> 10 个请求</span>
            StatIntervalInMs: <span style="color: #800080;">1000</span>, <span style="color: #008000;">//</span><span style="color: #008000;"> 1 秒之内</span>
            TokenCalculateStrategy: flow.Direct, <span style="color: #008000;">//</span><span style="color: #008000;"> 规定时间内，只能有多少请求</span>
            ControlBehavior:        flow.Reject, <span style="color: #008000;">//</span><span style="color: #008000;"> 超出的流量全部拒绝</span>
<span style="color: #000000;">        },
    })
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 循环接收请求</span>
    <span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">13</span>; i++<span style="color: #000000;"> {
        e,b :</span>= sentinel.Entry(<span style="color: #800000;">"</span><span style="color: #800000;">some-test</span><span style="color: #800000;">"</span>,sentinel.WithTrafficType(<span style="color: #0000ff;">base</span><span style="color: #000000;">.Inbound))
        </span><span style="color: #0000ff;">if</span> b !=<span style="color: #000000;"> nil {
            fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">限流了</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
            fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">正常通过</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            e.Exit()
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
