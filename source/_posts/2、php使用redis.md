---
title: "2、php使用redis"
date: "2021-02-23 14:33:00"
updated: "2021-02-23 16:08:00"
tags:
categories:
description: >-
  php安装扩展 若是phpstudy，打开扩展即可 连接远程redis，需要远程redis添加本机ip 配置文件69行加入 218.20.9.99 连接redis <?php //连接本地的 Redis 服务 $redis = new Redis(); $redis->connect('127.0.
---

<p><a href="https://www.runoob.com/redis/redis-php.html" target="_blank">php安装扩展</a></p>
<p>若是phpstudy，打开扩展即可</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210223142047958-1838904042.png" alt="" width="354" height="358" loading="lazy" /></p>
<p>&nbsp;</p>
<p>连接远程redis，需要远程redis添加本机ip</p>
<p>配置文件69行加入</p>
<div class="cnblogs_code">
<pre>218.20.9.99</pre>
</div>
<p>&nbsp;</p>
<p>连接redis</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php
    </span><span style="color: #008000;">//</span><span style="color: #008000;">连接本地的 Redis 服务</span>
   <span style="color: #800080;">$redis</span> = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Redis();
   </span><span style="color: #800080;">$redis</span>-&gt;connect('127.0.0.1', 6379<span style="color: #000000;">);
   </span><span style="color: #0000ff;">echo</span> "Connection to server successfully"<span style="color: #000000;">;
         </span><span style="color: #008000;">//</span><span style="color: #008000;">查看服务是否运行</span>
   <span style="color: #0000ff;">echo</span> "Server is running: " . <span style="color: #800080;">$redis</span>-&gt;<span style="color: #000000;">ping();
</span>?&gt;</pre>
</div>
<p>&nbsp;</p>
<p>实际运用</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php
    </span><span style="color: #008000;">//</span><span style="color: #008000;">连接本地的 Redis 服务</span>
    <span style="color: #800080;">$redis</span> = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Redis();
    </span><span style="color: #800080;">$redis</span>-&gt;connect('127.0.0.1', 6379<span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">字符串实例</span>
    <span style="color: #800080;">$redis</span>-&gt;set('iam_key','iam_value'<span style="color: #000000;">);
    </span><span style="color: #0000ff;">echo</span> "获取iam_key为：{<span style="color: #800080;">$redis</span>-&gt;get('iam_key')}"<span style="color: #000000;">;
    </span><span style="color: #0000ff;">echo</span> "&lt;br&gt;"<span style="color: #000000;">;

    </span><span style="color: #008000;">//</span><span style="color: #008000;">列表实例</span>
    <span style="color: #800080;">$redis</span>-&gt;lpush('ilist','123'<span style="color: #000000;">);
    </span><span style="color: #800080;">$redis</span>-&gt;lpush('ilist','456'<span style="color: #000000;">);
    </span><span style="color: #800080;">$redis</span>-&gt;lpush('ilist','789'<span style="color: #000000;">);
    </span><span style="color: #800080;">$redis</span>-&gt;lpush('ilist','987'<span style="color: #000000;">);
    </span><span style="color: #800080;">$redis</span>-&gt;lpush('ilist','654'<span style="color: #000000;">);
    </span><span style="color: #800080;">$redis</span>-&gt;lpush('ilist','321'<span style="color: #000000;">);
    </span><span style="color: #008080;">print_r</span>(<span style="color: #800080;">$redis</span>-&gt;lrange("ilist",0,5<span style="color: #000000;">));
    </span><span style="color: #0000ff;">echo</span> "&lt;br&gt;"<span style="color: #000000;">;

    </span><span style="color: #008000;">//</span><span style="color: #008000;">查询所有的key值</span>
    <span style="color: #008080;">print_r</span>(<span style="color: #800080;">$redis</span>-&gt;keys("*"<span style="color: #000000;">));
</span>?&gt;</pre>
</div>
<p>&nbsp;</p>
