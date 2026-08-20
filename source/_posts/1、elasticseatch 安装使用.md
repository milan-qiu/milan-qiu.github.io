---
title: "1、elasticseatch 安装使用"
date: "2022-02-18 21:13:00"
updated: "2022-02-20 09:37:00"
tags:
categories:
description: >-
  简述 es采用 倒排索引规则 新增数据时，会将数据进行 分词存储，并将分词对应的 位置记录下来 索引数据时，会将 索引关键词进行 分词拆分，后根据分词查找对应所在位置 安装es 创建 es 挂载的文件夹 mkdir -p /d/elasticsearch/config mkdir -p /d/ela
---

<h2>简述</h2>
<p>es采用 倒排索引规则</p>
<p>新增数据时，会将数据进行 分词存储，并将分词对应的 位置记录下来</p>
<p>索引数据时，会将 索引关键词进行 分词拆分，后根据分词查找对应所在位置</p>
<p>&nbsp;</p>
<h2>安装es</h2>
<p>创建 es 挂载的文件夹</p>
<div class="cnblogs_code">
<pre>mkdir -p /d/elasticsearch/<span style="color: #000000;">config
mkdir </span>-p /d/elasticsearch/<span style="color: #000000;">data
mkdir </span>-p /d/elasticsearch/plugins</pre>
</div>
<p>&nbsp;</p>
<p>写入配置文件</p>
<div class="cnblogs_code">
<pre> echo <span style="color: #800000;">"</span><span style="color: #800000;">http.host: 0.0.0.0</span><span style="color: #800000;">"</span> &gt;&gt; /d/elasticsearch/config/elasticsearch.yml</pre>
</div>
<p>&nbsp;</p>
<p>linux 安装并启动</p>
<div class="cnblogs_code">
<pre>docker run --name elasticsearch -d -e ES_JAVA_OPTS=<span style="color: #800000;">"</span><span style="color: #800000;">-Xms512m -Xmx512m</span><span style="color: #800000;">"</span> -e <span style="color: #800000;">"</span><span style="color: #800000;">discovery.type=single-node</span><span style="color: #800000;">"</span> -v /d/elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /d/elasticsearch/data:/usr/share/elasticsearch/data -v /d/elasticsearch/plugins:/usr/share/elasticsearch/plugins -p <span style="color: #800080;">9200</span>:<span style="color: #800080;">9200</span> -p <span style="color: #800080;">9300</span>:<span style="color: #800080;">9300</span> elasticsearch:<span style="color: #800080;">7.10</span>.<span style="color: #800080;">1</span></pre>
</div>
<p>windwos cmd窗口 安装启动</p>
<div class="cnblogs_code">
<pre>docker run --name elasticsearch -<span style="color: #000000;">d \
</span>-e ES_JAVA_OPTS=<span style="color: #800000;">"</span><span style="color: #800000;">-Xms512m -Xmx512m</span><span style="color: #800000;">"</span><span style="color: #000000;"> \
</span>-e <span style="color: #800000;">"</span><span style="color: #800000;">discovery.type=single-node</span><span style="color: #800000;">"</span><span style="color: #000000;"> \
</span>-v d:\elasticsearch\config\elasticsearch.yml:/usr/share/elasticsearch/config/<span style="color: #000000;">elasticsearch.yml \
</span>-v d:\elasticsearch\data:/usr/share/elasticsearch/<span style="color: #000000;">data \
</span>-v d:\elasticsearch\plugins:/usr/share/elasticsearch/<span style="color: #000000;">plugins \
</span>-p <span style="color: #800080;">9200</span>:<span style="color: #800080;">9200</span> -p <span style="color: #800080;">9300</span>:<span style="color: #800080;">9300</span><span style="color: #000000;"> \
elasticsearch:</span><span style="color: #800080;">7.10</span>.<span style="color: #800080;">1</span></pre>
</div>
<p>&nbsp;</p>
<p>验证是否成功</p>
<p><a href="http://localhost:9200" target="_blank">http://localhost:9200</a></p>
<p>&nbsp;</p>
<h2>安装kibana</h2>
<p>新建 kibana 映射目录</p>
<div class="cnblogs_code">
<pre>mkdir -p /d/kibana/config/</pre>
</div>
<p>&nbsp;</p>
<p>后创建配置文件</p>
<div class="cnblogs_code">
<pre>vim /d/kibana/config/kibana.yml</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">#
# </span>** THIS IS AN AUTO-GENERATED FILE **<span style="color: #000000;">
#

# Default Kibana configuration </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> docker target
server.name: kibana
server.host: </span><span style="color: #800000;">"</span><span style="color: #800000;">0</span><span style="color: #800000;">"</span><span style="color: #000000;">
elasticsearch.hosts: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">http://172.31.224.1:9200</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
xpack.monitoring.ui.container.elasticsearch.enabled: </span><span style="color: #0000ff;">true</span></pre>
</div>
<p>&nbsp;</p>
<p>windows cmd窗口 安装启动</p>
<div class="cnblogs_code">
<pre>docker run -<span style="color: #000000;">d \
  </span>--name=<span style="color: #000000;">kibana \
  </span>--restart=<span style="color: #000000;">always \
  </span>-p <span style="color: #800080;">5601</span>:<span style="color: #800080;">5601</span><span style="color: #000000;"> \
  </span>-v d:\kibana\config\kibana.yml:/usr/share/kibana/config/<span style="color: #000000;">kibana.yml \
  kibana:</span><span style="color: #800080;">7.10</span>.<span style="color: #800080;">1</span></pre>
</div>
<p>linux 启动</p>
<div class="cnblogs_code">
<pre>docker run -d --name kibana -e ELASTICKSEARCH_HOST=<span style="color: #800000;">"</span><span style="color: #800000;">http://172.31.224.1:9200</span><span style="color: #800000;">"</span> -p <span style="color: #800080;">5601</span>:<span style="color: #800080;">5601</span> kibana:<span style="color: #800080;">7.10</span>.<span style="color: #800080;">1</span></pre>
</div>
<p>&nbsp;</p>
<p>验证是否成功</p>
<p><a href="http://localhost:5601" target="_blank">http://localhost:5601</a></p>
<p>&nbsp;</p>
<p>若是配置文件挂载不成功就进入容器手动更改</p>
<div class="cnblogs_code">
<pre>docker exec -<span style="color: #000000;">it kibana bash

vim </span>/usr/share/kibana/config/kibana.yml</pre>
</div>
<p>&nbsp;</p>
<p>kibana 日志</p>
<div class="cnblogs_code">
<pre>docker logs -f kibana</pre>
</div>
<p>&nbsp;</p>
