---
title: "2、Docker 中部署 MongoDB"
date: "2022-02-24 19:04:00"
tags:
categories:
description: >-
  启用Mongo 拉取 mongodb 镜像 docker pull mongo 查看本地拉取的镜像 docker images 创建文件夹 mkdir mongodb cd ./mongodb mkdir data # 放置数据文件 mkdir backup # 备份文件 mkdir conf #
---

<h3><span style="font-size: 1.5em;">启用Mongo</span></h3>
<p>拉取 mongodb 镜像</p>
<div class="cnblogs_code">
<pre>docker pull mongo</pre>
</div>
<p>&nbsp;</p>
<p>查看本地拉取的镜像</p>
<div class="cnblogs_code">
<pre>docker images</pre>
</div>
<p>&nbsp;</p>
<p>创建文件夹</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">mkdir mongodb
cd .</span>/<span style="color: #000000;">mongodb
mkdir data # 放置数据文件
mkdir backup # 备份文件
mkdir conf # 配置文件</span></pre>
</div>
<p>&nbsp;</p>
<p>在 conf 目录下创建 mongodb.conf</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># mongodb.conf
logappend</span>=<span style="color: #0000ff;">true</span><span style="color: #000000;">
# bind_ip</span>=<span style="color: #800080;">127.0</span>.<span style="color: #800080;">0.1</span><span style="color: #000000;">
port</span>=<span style="color: #800080;">27017</span><span style="color: #000000;"> 
fork</span>=<span style="color: #0000ff;">true</span><span style="color: #000000;">
noprealloc</span>=<span style="color: #0000ff;">true</span><span style="color: #000000;">
auth</span>=<span style="color: #0000ff;">true</span></pre>
</div>
<p>&nbsp;</p>
<p>创建内部网络</p>
<div class="cnblogs_code">
<pre>docker network create tms</pre>
</div>
<p>&nbsp;</p>
<p>创建容器</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 创建容器</span>
docker run --name mongodb -v /dockerTest/mongodb/data:/data/db -v /dockerTest/mongodb/backup:/data/backup -v /dockerTest/mongodb/conf:/data/configdb -p <span style="color: #800080;">27018</span>:<span style="color: #800080;">27017</span> --network tms --network-alias mongodb -d mongo --<span style="color: #000000;">auth

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 命令解释</span>
docker run --name mongodb <span style="color: #008000;">//</span><span style="color: #008000;"> 容器命名mongodb</span>
-v /dockerTest/mongodb/data:/data/db <span style="color: #008000;">//</span><span style="color: #008000;"> 数据库数据文件挂载到/dockerTest/mongodb/data</span>
-v /dockerTest/mongodb/backup:/data/backup <span style="color: #008000;">//</span><span style="color: #008000;"> 备份文件挂载到/dockerTest/mongodb/backup</span>
-v /dockerTest/mongodb/conf:/data/configdb <span style="color: #008000;">//</span><span style="color: #008000;"> 启动的配置文件目录挂载到容器的/data/configdb</span>
-p <span style="color: #800080;">27018</span>:<span style="color: #800080;">27017</span> --network tms --network-<span style="color: #000000;">alias mongodb // 容器的27017端口，映射到主机的27018端口
</span>-d mongo --auth <span style="color: #008000;">//</span><span style="color: #008000;"> --auth开启身份验证</span></pre>
</div>
<p>&nbsp;</p>
<p>进入容器</p>
<div class="cnblogs_code">
<pre>winpty docker exec -it mongodb mongo admin</pre>
</div>
<p>&nbsp;</p>
<p>创建用户名和密码</p>
<div class="cnblogs_code">
<pre>db.createUser({ user:<span style="color: #800000;">'</span><span style="color: #800000;">admin</span><span style="color: #800000;">'</span>,pwd:<span style="color: #800000;">'</span><span style="color: #800000;">123456</span><span style="color: #800000;">'</span>,roles:[ { role:<span style="color: #800000;">'</span><span style="color: #800000;">userAdminAnyDatabase</span><span style="color: #800000;">'</span>, db: <span style="color: #800000;">'</span><span style="color: #800000;">admin</span><span style="color: #800000;">'</span>},<span style="color: #800000;">"</span><span style="color: #800000;">readWriteAnyDa</span>tabase<span style="color: #800000;">"</span><span style="color: #800000;">]});</span></pre>
</div>
<p>&nbsp;</p>
<p>测试连接</p>
<div class="cnblogs_code">
<pre>db.auth(<span style="color: #800000;">'</span><span style="color: #800000;">admin</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">123456</span><span style="color: #800000;">'</span>)</pre>
</div>
<p>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211205221815059-838346912.png" alt="" width="539" height="423" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;</h2>
<p>&nbsp;</p>
