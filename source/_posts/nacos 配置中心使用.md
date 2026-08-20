---
title: "nacos 配置中心使用"
date: "2022-03-09 17:41:00"
tags:
categories:
description: >-
  主要解决一个配置进行更改，所有实例都要进行配置重启的问题 命名空间：用来隔离配置，一般一个微服务一个命名空间 组：一般用来区分开发环境、测试环境、生产环境 nacos官方文档 docker 安装启动 docker run --name nacos-standalone -e MODE=standal
---

<p>主要解决一个配置进行更改，所有实例都要进行配置重启的问题</p>
<p>命名空间：用来隔离配置，一般一个微服务一个命名空间</p>
<p>组：一般用来区分开发环境、测试环境、生产环境</p>
<p><a href="https://nacos.io/zh-cn/docs/what-is-nacos.html" target="_blank">nacos官方文档</a></p>
<p>&nbsp;</p>
<p>docker 安装启动</p>
<div class="cnblogs_code">
<pre>docker run --name nacos-standalone -e MODE=standalone -e JVM_XMS=512m -e JVM_XMX=512m -e JVM_XMN=256m -p <span style="color: #800080;">8848</span>:<span style="color: #800080;">8848</span> -d nacos/nacos-server:latest</pre>
</div>
<p>&nbsp;</p>
<p>访问地址&nbsp;<a href="http://localhost:8848/nacos/index.html" target="_blank">http://localhost:8848/nacos/index.html</a></p>
<p>账号/密码：nacos/nacos</p>
<p>&nbsp;</p>
<p>go 读取 nacos，使用 <a href="https://github.com/nacos-group/nacos-sdk-go/blob/master/README_CN.md" target="_blank">nacos-sdk-go</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/nacos-group/nacos-sdk-go/clients</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/nacos-group/nacos-sdk-go/common/constant</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/nacos-group/nacos-sdk-go/vo</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">time</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 配置中心信息</span>
    serverConfigs :=<span style="color: #000000;"> []constant.ServerConfig{
        {
            IpAddr:      </span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.8</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            ContextPath: </span><span style="color: #800000;">"</span><span style="color: #800000;">/nacos</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Port:        </span><span style="color: #800080;">8848</span><span style="color: #000000;">,
            Scheme:      </span><span style="color: #800000;">"</span><span style="color: #800000;">http</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        },
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 客户端信息</span>
    clientConfig :=<span style="color: #000000;"> constant.ClientConfig{
        NamespaceId:         </span><span style="color: #800000;">"</span><span style="color: #800000;">85e41fdb-0887-48b0-b776-1f521e5c7a6d</span><span style="color: #800000;">"</span>, <span style="color: #008000;">//</span><span style="color: #008000;"> 如果需要支持多namespace，我们可以场景多个client,它们有不同的NamespaceId。当namespace是public时，此处填空字符串。</span>
        TimeoutMs:           <span style="color: #800080;">5000</span><span style="color: #000000;">,
        NotLoadCacheAtStart: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
        LogDir:              </span><span style="color: #800000;">"</span><span style="color: #800000;">tmp/nacos/log</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        CacheDir:            </span><span style="color: #800000;">"</span><span style="color: #800000;">tmp/nacos/cache</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        LogLevel:            </span><span style="color: #800000;">"</span><span style="color: #800000;">debug</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建动态配置客户端</span>
    configClient, err :=<span style="color: #000000;"> clients.NewConfigClient(
        vo.NacosClientParam{
            ClientConfig:  </span>&amp;<span style="color: #000000;">clientConfig,
            ServerConfigs: serverConfigs,
        },
    )

    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    </span><span style="color: #808080;">///</span><span style="color: #008000;">/ 获取配置</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">content, err := configClient.GetConfig(vo.ConfigParam{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    DataId: "config",
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    Group:  "prod"})
    </span><span style="color: #008000;">//</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">if err != nil {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    panic(err)
    </span><span style="color: #008000;">//</span><span style="color: #008000;">}
    </span><span style="color: #008000;">//</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">fmt.Println(content)

    </span><span style="color: #008000;">//</span><span style="color: #008000;">监听配置中心变化</span>
    err =<span style="color: #000000;"> configClient.ListenConfig(vo.ConfigParam{
        DataId: </span><span style="color: #800000;">"</span><span style="color: #800000;">config</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        Group:  </span><span style="color: #800000;">"</span><span style="color: #800000;">prod</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        OnChange: func(</span><span style="color: #0000ff;">namespace</span>, group, dataId, data <span style="color: #0000ff;">string</span><span style="color: #000000;">) {
            fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">group:</span><span style="color: #800000;">"</span> + group + <span style="color: #800000;">"</span><span style="color: #800000;">, dataId:</span><span style="color: #800000;">"</span> + dataId + <span style="color: #800000;">"</span><span style="color: #800000;">, data:</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> data)
        },
    })
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    time.Sleep(time.Hour)
}</span></pre>
</div>
<p>&nbsp;</p>
