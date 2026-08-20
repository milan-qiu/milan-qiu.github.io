---
title: "3、docker制作镜像"
date: "2022-02-24 19:05:00"
tags:
categories:
description: >-
  镜像具有 重复性 和 不可变性 下载并进入 golang 镜像 docker run -it golang:1.17 新建 Dockerfile 配置文件 # 启动编译环境 FROM golang:1.17 # 配置编译环境 RUN go env -w GO111MODULE=on RUN go e
---

<p>镜像具有 重复性 和 不可变性</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211219142633820-436975788.png" alt="" width="1050" height="238" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>下载并进入 golang 镜像</p>
<div class="cnblogs_code">
<pre>docker run -it golang:<span style="color: #800080;">1.17</span></pre>
</div>
<p>&nbsp;</p>
<p>新建 Dockerfile 配置文件</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 启动编译环境
FROM golang:</span><span style="color: #800080;">1.17</span><span style="color: #000000;">

# 配置编译环境
RUN go env </span>-w GO111MODULE=<span style="color: #000000;">on
RUN go env </span>-w GOPROXY=https:<span style="color: #008000;">//</span><span style="color: #008000;">goproxy.cn,direct</span>
<span style="color: #000000;">
# 拷贝源代码到镜像中
COPY .</span>/gateway /go/<span style="color: #000000;">src

# 编译
WORKDIR </span>/go/src/<span style="color: #000000;">gateway
RUN go install .</span>/<span style="color: #000000;">...

# 设置服务入口
ENTRYPOINT [ </span><span style="color: #800000;">"</span><span style="color: #800000;">/bin/gateway</span><span style="color: #800000;">"</span> ]</pre>
</div>
<p>&nbsp;</p>
<p>使用该文件</p>
<div class="cnblogs_code">
<pre>docker build -t package/name -f ./<span style="color: #000000;">Dockerfile .

</span><span style="color: #008000;">//</span><span style="color: #008000;"> package/name 表示生成后包的名称</span></pre>
</div>
<p>&nbsp;</p>
<p>测试生成后的东西</p>
<div class="cnblogs_code">
<pre>docker run package/name</pre>
</div>
<p>&nbsp;</p>
<p>Dockerfile命令</p>
<p><a href="https://www.runoob.com/docker/docker-dockerfile.html" target="_blank">https://www.runoob.com/docker/docker-dockerfile.html</a></p>
<p>&nbsp;</p>
<h3>Docker 镜像瘦身</h3>
<p>Dockerfile文件设置为</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 启动编译环境
FROM golang:</span><span style="color: #800080;">1.17</span>-<span style="color: #000000;">alpine AS builder

# 配置编译环境
RUN go env </span>-w GO111MODULE=<span style="color: #000000;">on
RUN go env </span>-w GOPROXY=https:<span style="color: #008000;">//</span><span style="color: #008000;">goproxy.cn,direct</span>
<span style="color: #000000;">
# 拷贝源代码到镜像中
COPY . </span>/go/src/coolcar/<span style="color: #000000;">server

# 编译
WORKDIR </span>/go/src/coolcar/<span style="color: #000000;">server
RUN go install .</span>/gateway/<span style="color: #000000;">...

FROM alpine:</span><span style="color: #800080;">3.15</span><span style="color: #000000;">
COPY </span>--<span style="color: #0000ff;">from</span>=builder /go/bin/gateway /bin/<span style="color: #000000;">gateway
ENV ADDR</span>=:<span style="color: #800080;">8080</span><span style="color: #000000;">

# 申明暴露的端口
EXPOSE </span><span style="color: #800080;">8080</span><span style="color: #000000;">

# 设置服务入口
ENTRYPOINT [ </span><span style="color: #800000;">"</span><span style="color: #800000;">/bin/gateway</span><span style="color: #800000;">"</span> ]</pre>
</div>
<p>&nbsp;</p>
