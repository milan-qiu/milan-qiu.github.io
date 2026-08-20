---
title: "1、prometheus + grafana 安装配置"
date: "2023-05-01 15:37:00"
updated: "2023-05-01 15:45:00"
tags:
categories:
description: >-
  开始安装 docker run -d --name=prometheus -p 9090:9090 prom/prometheus docker run -d --name=grafana -p 3000:3000 grafana/grafana docker run -d --name=node-
---

### 开始安装
```
docker run -d --name=prometheus -p 9090:9090 prom/prometheus

docker run -d --name=grafana -p 3000:3000 grafana/grafana

docker run -d --name=node-exporter -p 9100:9100 prom/node-exporter
```
prometheus是数据库，node-exporter是收集数据，grafana是展示数据

### 修改配置
进入prometheus容器 vi /etc/prometheus/prometheus.yml
找到job为prometheus的，将localhost改本机ip
后再添加一个job，用以监控服务器
```
  - job_name: linux
    static_configs:
    - targets: ['192.168.1.1:9100']         #被监控端的IP地址和端口号(有多个被监控端可用 逗号 隔开)
      labels:
        instance: localhost
```
后重启容器

### grafana添加数据源
访问 http://localhost:3000
首页找到 add your first datasource
搜索 prometheus 点击打开
填写 url，如 http://192.168.1.104:9090
save & test

### grafana 添加 dashboard
首页右上角 + 号，找到 import dashboard
grafana dashboard 市场地址：https://grafana.com/grafana/dashboards/
找到适合自己的 dashboard 后，复制id或json后，返回自己系统粘贴或上传
拉到最下，找到 prometheus 数据源
最后 import 完成（另外一个数据源同样操作）
