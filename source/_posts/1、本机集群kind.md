---
title: "1、本机集群kind"
date: "2021-12-19 13:11:00"
tags:
categories:
description: >-
  安装kubectl 1.22.4 安装kind（默认kubernetes版本为1.21.1） go install sigs.k8s.io/kind@v0.11.1 保持docker在运行状态，创建集群 kind create cluster 保存 kubernetes config 下来 kind
---

<p>安装<a href="https://kubernetes.io/zh/" target="_blank">kubectl</a></p>
<p><a href="https://storage.googleapis.com/kubernetes-release/release/v1.21.1/bin/windows/amd64/kubectl.exe" target="_blank">1.22.4</a></p>
<p>&nbsp;</p>
<p>安装<a href="https://kind.sigs.k8s.io/" target="_blank">kind</a>（默认kubernetes版本为1.21.1）</p>
<div class="cnblogs_code">
<pre>go install sigs.k8s.io/kind@v0.<span style="color: #800080;">11.1</span></pre>
</div>
<p>&nbsp;</p>
<p>保持docker在运行状态，创建集群</p>
<div class="cnblogs_code">
<pre>kind create cluster</pre>
</div>
<p>&nbsp;</p>
<p>保存 kubernetes config 下来</p>
<div class="cnblogs_code">
<pre>kind <span style="color: #0000ff;">get</span> kubeconfig &gt; ~/kubeconfig.config</pre>
</div>
<p>&nbsp;</p>
<p>vscode 通过 kubernetes 插件可以连接到各个集群</p>
<p>&nbsp;</p>
<p>命令行连接集群</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 设置集群地址文件</span>
export KUBECONFIG=~/<span style="color: #000000;">kubeconfig.config

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用</span>
kubectl cluster-<span style="color: #000000;">info

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除地址文件</span>
unset KUBECONFIG</pre>
</div>
<p>&nbsp;</p>
<h3>工作负载</h3>
<p><strong>Pod（逻辑上的物理主机）</strong></p>
<p>一般一个Pod运行一个conatianer。一个Pod运行多个container的话是sidecar模式</p>
<p>新建a.yaml文件，拉取镜像运行</p>
<div class="cnblogs_code">
<pre>apiVersion: apps/<span style="color: #000000;">v1
kind: Deployment
metadata:
  name: nginx</span>-<span style="color: #000000;">deployment
  labels:
    app: nginx
spec:
  replicas: </span><span style="color: #800080;">4</span><span style="color: #000000;">
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      </span>-<span style="color: #000000;"> name: nginx
        image: nginx
        ports:
        </span>- containerPort: <span style="color: #800080;">80</span><span style="color: #000000;">
        resources:
          limits:
            cpu: 100m
            memory: 128Mi</span></pre>
</div>
<p>运行</p>
<div class="cnblogs_code">
<pre>kubectl apply -f a.yaml</pre>
</div>
<p>查看当前运行的pods</p>
<div class="cnblogs_code">
<pre>kubectl <span style="color: #0000ff;">get</span> pods</pre>
</div>
<p>&nbsp;</p>
<p>利用插件，登录到pod实例</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211219120545333-1341509070.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>命令行登录到pod</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 先获取pod实例名称</span>
kubectl <span style="color: #0000ff;">get</span><span style="color: #000000;"> pods

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 登录进入</span>
kubectl exec -it nginx-deployment-8f6948fdf-6zrfz --<span style="color: #000000;"> sh

</span><span style="color: #008000;">//</span><span style="color: #008000;"> nginx-deployment-8f6948fdf-6zrfz  是 pod 名称</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>管理集群上的nginx服务</strong></p>
<p>新建b.yaml</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">apiVersion: v1
kind: Service
metadata:
  name: nginx</span>-<span style="color: #000000;">service
spec:
  selector:
    app: nginx
  ports:
    </span>-<span style="color: #000000;"> protocol: TCP
      port: </span><span style="color: #800080;">80</span></pre>
</div>
<p>执行</p>
<div class="cnblogs_code">
<pre>kubectl apply -f b.yaml </pre>
</div>
<p>查看集群运行的服务</p>
<div class="cnblogs_code">
<pre>kubectl <span style="color: #0000ff;">get</span> svc</pre>
</div>
<p>测试</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 登录远程</span>
kubectl exec -it nginx-deployment-8f6948fdf-6zrfz --<span style="color: #000000;"> sh

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 测试 nginx-service 有没有启动</span>
curl nginx-service</pre>
</div>
<p>&nbsp;</p>
<p><strong>Deployment</strong></p>
<p>删除集群上的 pods 及 deployment&nbsp;</p>
<div class="cnblogs_code">
<pre>kubectl delete deployment --<span style="color: #000000;">all

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 查看</span>
kubectl <span style="color: #0000ff;">get</span> pods</pre>
</div>
<p>&nbsp;</p>
<h3>集群物理层</h3>
<p>节点</p>
<p>kubernetes master</p>
<p>control plane</p>
<p>&nbsp;</p>
<h3>网络</h3>
<p>服务：基于DNS服务发现</p>
<p>负载均衡：基于iptable的负载均衡</p>
