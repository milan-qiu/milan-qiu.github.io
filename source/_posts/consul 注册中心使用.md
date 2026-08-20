---
title: "consul 注册中心使用"
date: "2022-03-09 15:09:00"
tags:
categories:
description: >-
  主要实现 分布式注册中心、服务注册、服务发现、健康检测 官方文档 开始安装运行 docker run -d -p 8500:8500 -p 8300:8300 -p 8301:8301 -p 8302:8302 -p 8600:8600/udp consul consul agent -dev -c
---

<p>主要实现 分布式注册中心、服务注册、服务发现、健康检测</p>
<p><a href="https://www.consul.io/docs" target="_blank">官方文档</a></p>
<p>&nbsp;</p>
<p>开始安装运行</p>
<div class="cnblogs_code">
<pre>docker run -d -p <span style="color: #800080;">8500</span>:<span style="color: #800080;">8500</span> -p <span style="color: #800080;">8300</span>:<span style="color: #800080;">8300</span> -p <span style="color: #800080;">8301</span>:<span style="color: #800080;">8301</span> -p <span style="color: #800080;">8302</span>:<span style="color: #800080;">8302</span> -p <span style="color: #800080;">8600</span>:<span style="color: #800080;">8600</span>/udp consul consul agent -dev -client=<span style="color: #800080;">0.0</span>.<span style="color: #800080;">0.0</span></pre>
</div>
<p>&nbsp;</p>
<p>修改为自启动</p>
<div class="cnblogs_code">
<pre>docker container update --restart=always consul</pre>
</div>
<p>&nbsp;</p>
<p>web界面打开注册中心：localhost:8500</p>
<p>dns服务器端口为 8600</p>
<p>&nbsp;</p>
<p>下载 <a href="https://www.isc.org/download/" target="_blank">bind 工具</a> 测试 dns 是否正常工作</p>
<div class="cnblogs_code">
<pre>dig @<span style="color: #800080;">127.0</span>.<span style="color: #800080;">0.1</span> -p <span style="color: #800080;">8600</span> consul.service.consul SRV</pre>
</div>
<p>&nbsp;</p>
<p>实践&nbsp;<a href="https://www.consul.io/api-docs/agent/service#register-service" target="_blank">服务注册</a>（可以配置 Check 进行健康检查）</p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202203/1680452-20220309100359420-1734171703.png" alt="" width="727" height="296" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>实践 <a href="https://www.consul.io/api-docs/agent/service#deregister-service" target="_blank">服务注销</a>（后面跟上是服务 Id）</p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202203/1680452-20220309101001835-252208478.png" alt="" width="780" height="171" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>web 层服务注册与发现</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package initialize

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/hashicorp/consul/api</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">sync</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

</span><span style="color: #0000ff;">var</span><span style="color: #000000;"> clientOnce sync.Once
</span><span style="color: #0000ff;">var</span> ConsulClient *<span style="color: #000000;">api.Client

</span><span style="color: #008000;">//</span><span style="color: #008000;"> GetConsulClient 实例化注册中心客户端</span>
func GetConsulClient() *<span style="color: #000000;">api.Client {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 连接注册中心</span>
<span style="color: #000000;">    clientOnce.Do(func() {
        cfg :</span>=<span style="color: #000000;"> api.DefaultConfig()
        cfg.Address </span>= <span style="color: #800000;">"</span><span style="color: #800000;">127.0.0.1:8500</span><span style="color: #800000;">"</span>

        <span style="color: #0000ff;">var</span><span style="color: #000000;"> err error
        
        ConsulClient,err </span>=<span style="color: #000000;"> api.NewClient(cfg)
        </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
            panic(err)
        }
    })
    
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> ConsulClient
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> ConsulRegister 开始注册</span>
func ConsulRegister(address <span style="color: #0000ff;">string</span>, port <span style="color: #0000ff;">int</span>,name <span style="color: #0000ff;">string</span>,tags []<span style="color: #0000ff;">string</span>,id <span style="color: #0000ff;">string</span><span style="color: #000000;">) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 生成注册对象</span>
    register := <span style="color: #0000ff;">new</span><span style="color: #000000;">(api.AgentServiceRegistration)
    register.Name </span>=<span style="color: #000000;"> name
    register.ID </span>=<span style="color: #000000;"> id
    register.Port </span>=<span style="color: #000000;"> port
    register.Tags </span>=<span style="color: #000000;"> tags
    register.Address </span>=<span style="color: #000000;"> address

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 生成对应的检查对象</span>
    check := &amp;<span style="color: #000000;">api.AgentServiceCheck{
        HTTP: </span><span style="color: #800000;">"</span><span style="color: #800000;">http://192.168.1.8:8080/health</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        Timeout: </span><span style="color: #800000;">"</span><span style="color: #800000;">5s</span><span style="color: #800000;">"</span>, <span style="color: #008000;">//</span><span style="color: #008000;"> 超时</span>
        Interval: <span style="color: #800000;">"</span><span style="color: #800000;">5s</span><span style="color: #800000;">"</span>, <span style="color: #008000;">//</span><span style="color: #008000;"> 检查间隔</span>
        DeregisterCriticalServiceAfter: <span style="color: #800000;">"</span><span style="color: #800000;">10s</span><span style="color: #800000;">"</span>, <span style="color: #008000;">//</span><span style="color: #008000;">注册失败10s后取消注册</span>
<span style="color: #000000;">    }
    register.Check </span>=<span style="color: #000000;"> check

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开始注册</span>
    err :=<span style="color: #000000;"> GetConsulClient().Agent().ServiceRegister(register)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> ConsulServices 全部服务</span>
<span style="color: #000000;">func ConsulServices() {
    data,err :</span>=<span style="color: #000000;"> GetConsulClient().Agent().Services()
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    </span><span style="color: #0000ff;">for</span> key,value :=<span style="color: #000000;"> range data{
        fmt.Println(key,value)
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> ConsulFilter 服务过滤</span>
<span style="color: #000000;">func ConsulFilter() {
    data,err :</span>= GetConsulClient().Agent().ServicesWithFilter(`Service == <span style="color: #800000;">"</span><span style="color: #800000;">micro-web1</span><span style="color: #800000;">"</span>`) <span style="color: #008000;">//</span><span style="color: #008000;"> 通过服务名称过滤</span>
    <span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    </span><span style="color: #0000ff;">for</span> key,value :=<span style="color: #000000;"> range data{
        fmt.Println(key,value)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
