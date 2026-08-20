---
title: "1、Redis基础"
date: "2021-02-23 14:08:00"
tags:
categories:
description: >-
  基本使用 连接 进入redis安装目录开启服务（后面指定用哪个配置文件运行） redis-server.exe redis.windows.conf 另外开窗口进行连接，第一种 redis-cli.exe -h 127.0.0.1 -p 6379 连接本地第二种方法 redis-cli //然后 p
---

<h2>基本使用</h2>
<h3>连接</h3>
<p>进入redis安装目录开启服务（后面指定用哪个配置文件运行）</p>
<div class="cnblogs_code">
<pre>redis-server.exe redis.windows.conf</pre>
</div>
<p>另外开窗口进行连接，第一种</p>
<div class="cnblogs_code">
<pre>redis-cli.exe -h 127.0.0.1 -p 6379</pre>
</div>
<p>连接本地第二种方法</p>
<div class="cnblogs_code">
<pre>redis-<span style="color: #000000;">cli
</span><span style="color: #008000;">//</span><span style="color: #008000;">然后</span>
ping</pre>
</div>
<p>&nbsp;</p>
<p>连接远程redis</p>
<div class="cnblogs_code">
<pre>redis-cli -h host -p port -a password</pre>
</div>
<p>&nbsp;</p>
<h3>key</h3>
<p><a href="%20http://www.redis.cn/commands.html#generic" target="_blank">key命令大全</a></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">删除key</span>
DEL <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">检测key是否存在</span>
EXISTS <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">查找所有符合给定模式( pattern)的 key </span>
<span style="color: #000000;">KEYS pattern

</span><span style="color: #008000;">//</span><span style="color: #008000;">序列化key，并返回序列化之后的值</span>
DUMP <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">给key设置过期时间，以秒为单位</span>
EXPIRE <span style="color: #008080;">key</span> 86400

<span style="color: #008000;">//</span><span style="color: #008000;">移除key的过期时间</span>
PERSIST <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)</span>
TTL <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">从当前数据库中随机返回一个 key</span>
<span style="color: #000000;">RANDOMKEY

</span><span style="color: #008000;">//</span><span style="color: #008000;">修改 key 的名称</span>
<span style="color: #008080;">RENAME</span> <span style="color: #008080;">key</span><span style="color: #000000;"> newkey

</span><span style="color: #008000;">//</span><span style="color: #008000;">仅当 newkey 不存在时，将 key 改名为 newkey</span>
RENAMENX <span style="color: #008080;">key</span><span style="color: #000000;"> newkey

</span><span style="color: #008000;">//</span><span style="color: #008000;">返回 key 所储存的值的类型</span>
TYPE <span style="color: #008080;">key</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>String（字符串）</h3>
<p><a href="http://www.redis.cn/commands.html#string" target="_blank">string命令</a></p>
<div class="cnblogs_code">
<pre>set a '哈哈哈哈'<span style="color: #000000;">
get a
</span><span style="color: #008000;">//</span><span style="color: #008000;">a最大可以存储512MB</span>


<span style="color: #008000;">//</span><span style="color: #008000;">////////////  设置/获取   //////////////
//设置key</span>
SET <span style="color: #008080;">key</span><span style="color: #000000;"> value

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取key</span>
GET <span style="color: #008080;">key</span>


<span style="color: #008000;">//</span><span style="color: #008000;">设置key，当key不存在时</span>
SETNX <span style="color: #008080;">key</span><span style="color: #000000;"> value

</span><span style="color: #008000;">//</span><span style="color: #008000;">设置多个key</span>
<span style="color: #000000;">MSET key1 value1 key2 value2

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取多个key</span>
<span style="color: #000000;">MGET key1 key2

</span><span style="color: #008000;">//</span><span style="color: #008000;">设置多个key，仅当key不存在时</span>
<span style="color: #000000;">MSETNX key1 value1 key2 value2


</span><span style="color: #008000;">//</span><span style="color: #008000;">////////////  功能性  //////////////
//返回key的长度</span>
<span style="color: #008080;">STRLEN</span> <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">将 key 中储存的数字值增一</span>
INCR <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">将 key 中储存的数字值减一</span>
DECR <span style="color: #008080;">key</span>

<span style="color: #008000;">//</span><span style="color: #008000;">如果 key 已经存在并且是一个字符串，就会追加到value末尾</span>
APPEND <span style="color: #008080;">key</span> value</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>&nbsp;</h3>
<h3>Hash（哈希）</h3>
<p><a href="http://www.redis.cn/commands.html#hash" target="_blank">hash命令</a></p>
<div class="cnblogs_code">
<pre>HMSET b field1 "Hello" field2 "World"<span style="color: #000000;">
HGET b field1
HGET b field2
</span><span style="color: #008000;">//</span><span style="color: #008000;">每个 hash 可以存储 232 -1 键值对（40多亿）</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>List（列表）</h3>
<p><a href="http://www.redis.cn/commands.html#list" target="_blank">list命令</a></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">给d列表赋值添加</span>
<span style="color: #000000;">lpush d a1
lpush d a2
lpush d a3
lpush d a4

</span><span style="color: #008000;">//</span><span style="color: #008000;">输出d列表 0-10 项的信息</span>
lrange d 0 10
<span style="color: #008000;">//</span><span style="color: #008000;">列表最多可存储 232 - 1 元素 (4294967295, 每个列表可存储40多亿)</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>Set（集合）</h3>
<p><a href="http://www.redis.cn/commands.html#set" target="_blank">set命令</a></p>
<p>string 类型的无序集合。</p>
<p>集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。</p>
<p><strong>sadd 命令：</strong>添加一个 string 元素到 key 对应的 set 集合中，成功返回 1，如果元素已经在集合中返回 0。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">添加到集合e</span>
<span style="color: #000000;">sadd e e1
sadd e e2
sadd e e3
sadd e e4
sadd e e5

</span><span style="color: #008000;">//</span><span style="color: #008000;">查询集合e</span>
<span style="color: #000000;">smembers e
</span><span style="color: #008000;">//</span><span style="color: #008000;">集合中最大的成员数为 232 - 1(4294967295, 每个集合可存储40多亿个成员)</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>zset(sorted set：有序集合)</h3>
<p><a href="http://www.redis.cn/commands.html#sorted_set" target="_blank">sorted set 命令</a></p>
<p>Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。</p>
<p>不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。</p>
<p>zset的成员是唯一的,但分数(score)却可以重复</p>
<p><strong>zadd 命令:</strong>添加元素到集合，元素在集合中存在则更新对应score</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">添加到集合f</span>
zadd f 0<span style="color: #000000;"> f1
zadd f </span>0<span style="color: #000000;"> f2
zadd f </span>0<span style="color: #000000;"> f3
zadd f </span>0<span style="color: #000000;"> f3

</span><span style="color: #008000;">//</span><span style="color: #008000;">查询集合f</span>
ZRANGEBYSCORE f 0 1000</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>订阅与发布</h3>
<p>订阅者监听频道</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">订阅chanal频道</span>
SUBCRIBE chanal</pre>
</div>
<p>&nbsp;</p>
<p>发布者，打开另一个窗口</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">发布消息</span>
PUBLISH chanal &ldquo;hahahah&rdquo;</pre>
</div>
<p>&nbsp;</p>
<p>然后订阅者就能收到消息</p>
<p>&nbsp;</p>
<h3>Redis事务</h3>
<ul>
<li>开始事务。</li>
<li>命令入队。</li>
<li>执行事务。</li>
</ul>
<p>开始事务</p>
<div class="cnblogs_code">
<pre>MULTI</pre>
</div>
<p>&nbsp;</p>
<p>命令入队</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">SET a bbb
GET a
MSET b bbb c ccc d ddd
MGET a b c d</span></pre>
</div>
<p>&nbsp;</p>
<p>执行事务</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">EXEC</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>Redis脚本</h3>
<p>Redis 脚本使用 Lua 解释器来执行脚本。 Redis 2.6 版本通过内嵌支持 Lua 环境。执行脚本的常用命令为&nbsp;<strong>EVAL</strong></p>
<p><strong><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210223135709092-244430457.png" alt="" width="548" height="401" loading="lazy" /></strong></p>
<p>&nbsp;</p>
<h3>Redis连接</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">验证密码是否正确</span>
AUTH "password"

<span style="color: #008000;">//</span><span style="color: #008000;">服务器是否正常</span>
PING</pre>
</div>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210223140055249-1689328718.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>Redis服务器</h3>
<p><a href="http://www.redis.cn/commands.html#server" target="_blank">redis服务器命令</a></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">查看服务器信息</span>
INFO</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>Redis GEO</h3>
<p>略。</p>
<p>&nbsp;</p>
<h3>Redis Stream</h3>
<p>略。</p>
