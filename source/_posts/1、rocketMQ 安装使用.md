---
title: "1、rocketMQ 安装使用"
date: "2022-02-20 22:55:00"
updated: "2022-02-20 23:15:00"
tags:
categories:
description: >-
  RocketMQ 安装 获取镜像 docker pull foxiswho/rocketmq:server-4.3.2 docker pull foxiswho/rocketmq:broker-4.3.2 创建挂载目录 mkdir -p /d/mqserver/logs mkdir -p /d/mq
---

<h2>RocketMQ 安装</h2>
<p>获取镜像</p>
<div class="cnblogs_code">
<pre>docker pull foxiswho/rocketmq:server-<span style="color: #800080;">4.3</span>.<span style="color: #800080;">2</span><span style="color: #000000;"> 
docker pull foxiswho</span>/rocketmq:broker-<span style="color: #800080;">4.3</span>.<span style="color: #800080;">2</span></pre>
</div>
<p>&nbsp;</p>
<p>创建挂载目录</p>
<div class="cnblogs_code">
<pre>mkdir -p /d/mqserver/<span style="color: #000000;">logs
mkdir </span>-p /d/mqserver/<span style="color: #000000;">store
mkdir </span>-p /d/mqbroker/<span style="color: #000000;">logs
mkdir </span>-p /d/mqbroker/<span style="color: #000000;">store
mkdir </span>-p /d/mqbroker/conf</pre>
</div>
<p>&nbsp;</p>
<h4>创建配置文件&nbsp;/d/mqbroker/conf/broker.conf</h4>
<div class="cnblogs_code">
<pre>namesrvAddr=<span style="color: #800080;">172.31</span>.<span style="color: #800080;">224.1</span>:<span style="color: #800080;">9876</span><span style="color: #000000;">
brokerClusterName </span>=<span style="color: #000000;"> DefaultCluster
brokerName </span>= broker-<span style="color: #000000;">a
brokerId </span>= <span style="color: #800080;">0</span><span style="color: #000000;">
deleteWhen </span>= <span style="color: #800080;">04</span><span style="color: #000000;">
fileReservedTime </span>= <span style="color: #800080;">48</span><span style="color: #000000;">
brokerRole </span>=<span style="color: #000000;"> ASYNC_MASTER
flushDiskType </span>=<span style="color: #000000;"> ASYNC_FLUSH
brokerIP1 </span>= <span style="color: #800080;">192.168</span>.<span style="color: #800080;">130.128</span><span style="color: #000000;">
listenPort</span>=<span style="color: #800080;">10911<br /></span></pre>
<div>&nbsp; transientStorePoolEnable=true</div>
<pre><span style="color: #800080;">&nbsp;</span></pre>
</div>
<p>&nbsp;</p>
<p>启动 server 容器</p>
<div class="cnblogs_code">
<pre>docker run -it -d --name mqserver -p <span style="color: #800080;">9876</span>:<span style="color: #800080;">9876</span> -e <span style="color: #800000;">"</span><span style="color: #800000;">JAVA_OPT_EXT=-server -Xms128m -Xmx128m -Xmn128m</span><span style="color: #800000;">"</span> -e <span style="color: #800000;">"</span><span style="color: #800000;">JAVA_OPTS=-Duser.home=/opt</span><span style="color: #800000;">"</span> -v d:\mqserver\logs:/opt/logs -v d:\mqserver/store:/opt/store foxiswho/rocketmq:server-<span style="color: #800080;">4.3</span>.<span style="color: #800080;">2</span></pre>
</div>
<p>&nbsp;</p>
<p>启动 broker 容器</p>
<div class="cnblogs_code">
<pre>docker run -d -p <span style="color: #800080;">10911</span>:<span style="color: #800080;">10911</span> -p <span style="color: #800080;">10909</span>:<span style="color: #800080;">10909</span> --name mqbroker -e <span style="color: #800000;">"</span><span style="color: #800000;">JAVA_OPT_EXT=-server -Xms128m -Xmx128m -Xmn128m</span><span style="color: #800000;">"</span> -e <span style="color: #800000;">"</span><span style="color: #800000;">JAVA_OPTS=-Duser.home=/opt</span><span style="color: #800000;">"</span> -v d:\mqbroker\conf\broker.conf:/etc/rocketmq/broker.conf -v d:\mqbroker\logs:/opt/logs -v d:\mqbroker\store:/opt/store --privileged=<span style="color: #0000ff;">true</span> foxiswho/rocketmq:broker-<span style="color: #800080;">4.3</span>.<span style="color: #800080;">2</span></pre>
</div>
<p>&nbsp;</p>
<h2>RocketMQ 管理工具安装</h2>
<p>获取镜像</p>
<div class="cnblogs_code">
<pre>docker pull styletang/rocketmq-console-ng:<span style="color: #800080;">1.0</span>.<span style="color: #800080;">0</span></pre>
</div>
<p>&nbsp;</p>
<p>启动 mqconsole 容器</p>
<div class="cnblogs_code">
<pre>docker run -it -d --name mqconsole -e <span style="color: #800000;">"</span><span style="color: #800000;">JAVA_OPTS=-Drocketmq.namesrv.addr=172.31.224.1:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false</span><span style="color: #800000;">"</span> -p <span style="color: #800080;">8080</span>:<span style="color: #800080;">8080</span> -t styletang/rocketmq-console-ng:<span style="color: #800080;">1.0</span>.<span style="color: #800080;">0</span></pre>
</div>
<p>&nbsp;</p>
<p>启动管理工具</p>
<p><a href="http://localhost:8080/#/" target="_blank">http://localhost:8080/#/</a></p>
<p>&nbsp;</p>
<p>尝试创建 topic 后，发送消息，接收消息</p>
<p>&nbsp;</p>
