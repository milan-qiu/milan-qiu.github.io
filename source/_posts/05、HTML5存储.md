---
title: "05、HTML5存储"
date: "2020-04-09 15:20:00"
updated: "2020-04-11 22:20:00"
tags:
categories:
description: >-
  HTML5存储 //一个比cookie更好的本地存储方式。 什么是 HTML5 Web 存储? 使用HTML5可以在本地存储用户的浏览数据。 早些时候,本地存储使用的是 cookie。但是Web 存储需要更加的安全与快速. 这些数据不会被保存在服务器上，但是这些数据只用于用户请求网站数据上.它也可以
---

<h2>HTML5存储</h2>
<p>//一个比cookie更好的本地存储方式。</p>
<p>&nbsp;</p>
<h3>什么是 HTML5 Web 存储?</h3>
<p>使用HTML5可以在本地存储用户的浏览数据。</p>
<p>早些时候,本地存储使用的是 cookie。但是Web 存储需要更加的安全与快速. 这些数据不会被保存在服务器上，但是这些数据只用于用户请求网站数据上.它也可以存储大量的数据，而不影响网站的性能.</p>
<p>数据以 键/值 对存在, web网页的数据只允许该网页访问使用。</p>
<p>&nbsp;</p>
<h3>localStorage 和 sessionStorage&nbsp;</h3>
<p>客户端存储数据的两个对象为：</p>
<ul>
<li>localStorage</li>
<li>- 用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去除。</li>
<li>存储容量2-5M</li>
<li></li>
<li>sessionStorage</li>
<li>- 用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。</li>
<li>存储容量不一，部分浏览器不设限制</li>
</ul>
<p>在使用 web 存储前,应检查浏览器是否支持 localStorage 和sessionStorage:</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span>(<span style="color: #0000ff;">typeof</span>(Storage)!=="undefined"<span style="color: #000000;">)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 是的! 支持 localStorage  sessionStorage 对象!</span>
    <span style="color: #008000;">//</span><span style="color: #008000;"> 一些代码.....</span>
} <span style="color: #0000ff;">else</span><span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 抱歉! 不支持 web 存储。</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>判断浏览器是否支持HTML5存储</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span>(<span style="color: #0000ff;">typeof</span>(Storage)!=="undefined"<span style="color: #000000;">)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 是的! 支持 localStorage  sessionStorage 对象!</span>
    <span style="color: #008000;">//</span><span style="color: #008000;"> 一些代码.....</span>
} <span style="color: #0000ff;">else</span><span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 抱歉! 不支持 web 存储。</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>localStorage 对象</h3>
<p>//localStorage 对象存储的数据没有时间限制。第二天、第二周或下一年之后，数据依然可用。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 存储key为jj，value为"这个是jj属性的值"的数据</span>
localStorage.jj = "这个是jj属性的值"<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 查找jj属性对应的value</span>
alert(localStorage.jj) ;</pre>
</div>
<p>&nbsp;</p>
<p>localStorage的常用方法（换个session前缀也可用于sessionStorage）</p>
<ul>
<li>保存数据 (推荐)：localStorage.setItem(key,value);</li>
<li>保存数据：localStorage.key = value;</li>
<li>保存数据：localStorage[key] = value;</li>
<li></li>
<li>读取数据：localStorage.getItem(key);</li>
<li>删除单个数据：localStorage.removeItem(key);</li>
<li>删除所有数据：localStorage.clear();</li>
<li>得到某个索引的key：localStorage.key(index);</li>
</ul>
<p>Tip：&nbsp;键/值对通常以字符串存储，你可以按自己的需要转换该格式。</p>
<p>&nbsp;</p>
<h3>sessionStorage 对象</h3>
<p>//sessionStorage 方法针对一个 session 进行数据存储。当用户关闭浏览器窗口后，数据会被删除。</p>
<p>sessionStorage的属性方法同localStorage一样。实例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span> (sessionStorage.jj)    <span style="color: #008000;">//</span><span style="color: #008000;">判断sessionStorage的jj是否存在</span>
<span style="color: #000000;">{
    sessionStorage.jj</span>=Number(sessionStorage.jj)+1<span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">若存在就转换为数字，令其加一</span>
<span style="color: #000000;">}
</span><span style="color: #0000ff;">else</span><span style="color: #000000;">
{
    sessionStorage.jj</span>=1<span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">若不存在就定义一个</span>
<span style="color: #000000;">}
alert(</span>"执行了" + sessionStorage.jj + "次");</pre>
</div>
<p>&nbsp;</p>
<h2 id="page-title" class="asset-name entry-title">浏览器数据库 IndexedDB</h2>
<p>阮一峰教程：<a href="http://www.ruanyifeng.com/blog/2018/07/indexeddb.html">http://www.ruanyifeng.com/blog/2018/07/indexeddb.html</a></p>
<p>随着浏览器的功能不断增强，越来越多的网站开始考虑，将大量数据储存在客户端，这样可以减少从服务器获取数据，直接从本地获取数据。</p>
<ul>
<li>Cookie：存储大小不超过4KB。且每次请求都会发送回服务器；</li>
<li>LocalStorage： 存储大小在 2.5MB 到 10MB 之间（各家浏览器不同）。且不提供搜索功能，不能建立自定义的索引。</li>
<li>SessionStorage：存储大小不一（部分浏览器不设限制）。但在关闭窗口或标签页之后将会删除这些数据。</li>
<li>IndexedDB：存储大小不少于 250MB，甚至没有上限。</li>
</ul>
<p>&nbsp;</p>
<h3>打开数据库</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> request = window.indexedDB.open(databaseName, version);</pre>
</div>
<p>&nbsp;</p>
<p>//version版本号，可选参数 。</p>
<p>//若没有该数据库就创建，有就打开</p>
<h3>打开数据库成功（事件）</h3>
<div class="cnblogs_code">
<pre>request.onsuccess = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(数据库打开</span>/创建成功);
}</pre>
</div>
<p>&nbsp;</p>
<h3>打开数据库失败（事件）</h3>
<p>//版本号只能升级不能降级，否则数据库会打开失败</p>
<div class="cnblogs_code">
<pre>request.onerror = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(</span>"数据库打开/创建失败"<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>版本号已升级（事件）</h3>
<div class="cnblogs_code">
<pre>request.onupgradeneeded = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
console.log(</span>"版本号已升级"<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>创建表</h3>
<p>//需要版本号升级后，才能创建表</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">//将版本号升级为2<br />var</span> request = window.indexedDB.open('shujvming',2<span style="color: #000000;">);
<br /><br /></span><span style="color: #008000;">//</span><span style="color: #008000;">版本号升级成功后，才能创建表</span>
request.onupgradeneeded = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
</span><span style="color: #0000ff;">　　var</span> table =<span style="color: #000000;"> request.result;<br />　　//建表时要设置主键，如设置自增主键
　　table.createObjectStore(</span>'table1',{autoIncrement:true}<span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>设置主键（建表时操作）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">设置自增主键</span>
{autoIncrement: <span style="color: #0000ff;">true</span><span style="color: #000000;">}
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置某字段为主键</span>
{keyPath:'字段名'}</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>表数据的增删改查</h2>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">增加数据：IDBObjectStore.add<br /></span><span style="color: #008000;">
//</span><span style="color: #008000;">获取数据：IDBObjectStore.get</span><span style="color: #008000;">
//</span><span style="color: #008000;">获取全部数据：IDBObjectStore.getAll<br /><br />//修改数据：IDBObjectStore.put<br /><br />//删除数据：IDBObjectStore.del<br />//删除全部数据：IDBObjectStore.clear</span></pre>
</div>
<h3>增加数据</h3>
<div class="cnblogs_code">
<pre>function<span> add() {
    //选择需要操作的某个数据库
    var db =<span> request.result;

    //写入数据必须新建事务。
    var shiwu = db.transaction(['table1'], 'readwrite'); //指定表格名称和操作模式（"只读"或"读写"）。

    //选择需要操作的某个表
    var tb = shiwu.objectStore('table1'<span>);</span></span></span></pre>
<p>　　　 //执行插入内容<br />				　　　 var state = tb.add(tbshujv);<br />				<br />				　　　&nbsp;//插入成功后提示<br />				　　&nbsp; state.onsuccess = function(){<br />					　　&nbsp; 　　console.log("插入成功了");</p>
<p>　　　　　console.log(state.result); //执行成功后返回该条数据的key值</p>
<p>　　　}</p>
<pre><span><span><span><span>
setTimeout(function<span>() {
    add();
}, 300)</span></span></span></span></span></pre>
</div>
<h3>&nbsp;查找数据</h3>
<p>//通过key值，查找该条数据</p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
</span><span style="color: #0000ff;">　　var</span> db =<span style="color: #000000;"> request.result;
</span><span style="color: #0000ff;">　　var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
</span><span style="color: #0000ff;">　　var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);
</span><span style="color: #008000;">　　/</span><span style="color: #008000;"> 获取数据</span>
<span style="color: #0000ff;">　　var</span> tbNode = tb.get(1<span style="color: #000000;">);
　　tbNode.onsuccess </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
　　　　console.log(tbNode.result);
　　}
}, </span>300)</pre>
</div>
<p>//获取所有数据，result是以数据形式表现</p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
　　</span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
　　</span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
　　</span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);
　　</span><span style="color: #008000;">//</span><span style="color: #008000;"> 获取所有数据</span>
　　<span style="color: #0000ff;">var</span> tbNode =<span style="color: #000000;"> tb.getAll();
　　tbNode.onsuccess </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
　　　　console.log(tbNode.result);
　　}
}, </span>300)</pre>
</div>
<h3>修改 / 增加数据&nbsp;</h3>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
　　</span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
　　</span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
　　</span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);
　　</span><span style="color: #008000;">//</span><span style="color: #008000;"> 修改 / 增加数据</span>
　　<span style="color: #0000ff;">var</span> tbNode =<span style="color: #000000;"> tb.put({
           </span>"id":102<span style="color: #000000;">,
           </span>"name":"zhanag"<span style="color: #000000;">,
            </span>"bb":"bb"<span style="color: #000000;">
      });
}, </span>300)    </pre>
</div>
<p>&nbsp;</p>
<h3>删除数据</h3>
<p>//通过key值，删除该条数据</p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
　　</span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
　　</span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
　　</span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);
　　</span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除数据</span>
　　tb.del(1); <span style="color: #008000;">//</span><span style="color: #008000;">删除key值为1的那条数据</span>
}, 300)    </pre>
</div>
<p>&nbsp;</p>
<p>//删除所有数据</p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
　　</span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
　　</span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
　　</span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);
　　</span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除所有数据</span>
<span style="color: #000000;">　　tb.clear(); 
}, </span>300)  </pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>indexedDB索引</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">IDBObjectStore.createIndex
indexName：索引名称（表名）
keyPath：索引字段，可以为空或数组。（表字段）
optionParameters：索引配置参数（字段是否重复）</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;//刚建完表后&nbsp; 就可以创建索引</p>
<div class="cnblogs_code">
<pre>request.onupgradeneeded = <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
    </span><span style="color: #0000ff;">var</span> table = request.result;<span style="color: #008000;">//</span><span style="color: #008000;">选择数据库</span>
    <span style="color: #0000ff;">var</span> store = table.createObjectStore('table1', {autoIncrement: <span style="color: #0000ff;">true</span><span style="color: #000000;">});
    </span><span style="color: #008000;">//</span><span style="color: #008000;">设置索引</span>
    store.createIndex('table1','name',{unique:<span style="color: #0000ff;">false</span><span style="color: #000000;">}); //若unique为true，字段就不能重复，否则数据库就不写入内容
}</span></pre>
</div>
<p>&nbsp;</p>
<p>//获取索引值&nbsp; 所对应的那条数据</p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    </span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
    </span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
    </span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">获取索引值所对应的那条数据</span>
    <span style="color: #0000ff;">var</span> index = tb.index('table1'); <span style="color: #008000;">//</span><span style="color: #008000;">选择表</span>
    index.get('zhang').onsuccess = <span style="color: #0000ff;">function</span><span style="color: #000000;">(event) {
        console.log(event.target.result);
    }
},</span>300)</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>游标</h2>
<p>//能更好地获取表格数据（不通过索引值方式）</p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    </span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
    </span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
    </span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">通过游标获取数据</span>
    <span style="color: #0000ff;">var</span> you = tb.openCursor(IDBKeyRange.only(1)); <span style="color: #008000;">//</span><span style="color: #008000;">仅获取key值为1的索引数据</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">获取成功后打印出来</span>
    you.onsuccess = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
        console.log(you.result.value);
    };
},</span>300)</pre>
</div>
<p>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200411172610063-798837232.png" alt="" /></p>
<h3>遍历</h3>
<p>//输出key小于等于2的数据（ upperBound(x) ）</p>
<div class="cnblogs_code">
<pre>setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
    </span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
    </span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
    </span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">通过游标获取数据</span>
    <span style="color: #0000ff;">var</span> you = tb.openCursor(IDBKeyRange.upperBound(2)); <span style="color: #008000;">//</span><span style="color: #008000;">获取key小于等于2的数据</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">可能返回多个IDBRequest对象。（IDBRequest -&gt; result -&gt; value，value对象才是数据）</span>

    <span style="color: #008000;">//</span><span style="color: #008000;">获取成功后打印出来</span>
    you.onsuccess = <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
        </span><span style="color: #0000ff;">if</span> (you.result) { <span style="color: #008000;">//</span><span style="color: #008000;">IDBRequest -&gt; result 里面才有循环方法</span>
<span style="color: #000000;">            console.log(you.result.value);
            you.result.</span><span style="color: #0000ff;">continue</span>(); <span style="color: #008000;">//</span><span style="color: #008000;">因为可能有多组数据，所以需要循环输出</span>
<span style="color: #000000;">        }
    };
}, </span>300)</pre>
</div>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200411180556615-932539877.png" alt="" /></p>
<p>//具体实现方法同上</p>
<h3>查询顺序（direction）</h3>
<p>//在获取数据时定义，默认正序next</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> you = tb.openCursor(IDBKeyRange.upperBound(2),'next');</pre>
</div>
<p>&nbsp;</p>
<p>//下面是倒序prev</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> you = tb.openCursor(IDBKeyRange.upperBound(2),'prev');</pre>
</div>
<p>&nbsp;</p>
<p>//另外还有：</p>
<p>顺序唯一查询：nextunique</p>
<p>倒序唯一查询：prevunique</p>
<p>&nbsp;</p>
<h2>索引跟游标结合&nbsp;</h2>
<p>//普通游标用的是key值，加了索引后就可以用其他值了</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">建完表创建索引</span>
store.createIndex('table1','age',{unique:<span style="color: #0000ff;">false</span><span style="color: #000000;">});

setTimeout(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">() {
    </span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> request.result;
    </span><span style="color: #0000ff;">var</span> shiwu = db.transaction(['table1'], 'readwrite'<span style="color: #000000;">);
    </span><span style="color: #0000ff;">var</span> tb = shiwu.objectStore('table1'<span style="color: #000000;">);
    
    </span><span style="color: #008000;">//</span><span style="color: #008000;">选择表</span>
    <span style="color: #0000ff;">var</span> index = tb.index('table1'<span style="color: #000000;">);    <br />/******* 上面是索引方法，下面是游标方法 *****************************************************/
    </span><span style="color: #008000;">//</span><span style="color: #008000;">通过游标获取数据（普通游标获取的是key值，现在通过索引更改成了age）</span>
    <span style="color: #0000ff;">var</span> you = tb.openCursor(IDBKeyRange.upperBound(18)); <span style="color: #008000;">//</span><span style="color: #008000;">age小于等于18的数据</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">获取成功后打印出来</span>
    you.onsuccess = <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
        </span><span style="color: #0000ff;">if</span> (you.result) { <span style="color: #008000;">//</span><span style="color: #008000;">IDBRequest -&gt; result 里面才有循环方法</span>
<span style="color: #000000;">            console.log(you.result.value);
            you.result.</span><span style="color: #0000ff;">continue</span>(); <span style="color: #008000;">//</span><span style="color: #008000;">因为可能有多组数据，所以需要循环输出</span>
<span style="color: #000000;">        }
    };
}, </span>300)</pre>
</div>
<p>&nbsp;</p>
<h3>更新数据</h3>
<div class="cnblogs_code">
<pre>you.onsuccess = <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
    </span><span style="color: #0000ff;">if</span> (you.result.value.name == 'zhangsan') { <span style="color: #008000;">//</span><span style="color: #008000;">获取name='zhangsan'的那条数据</span>
        you.result.update({    <span style="color: #008000;">//</span><span style="color: #008000;">执行更新</span>
            "id": 666<span style="color: #000000;">,
            </span>"name": "lisi"<span style="color: #000000;">,
            </span>"age": 80<span style="color: #000000;">,
            </span>"address": "shanghai"<span style="color: #000000;">
        })
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>删除数据</h3>
<div class="cnblogs_code">
<pre>you.onsuccess = <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
    </span><span style="color: #0000ff;">if</span> (you.result.value.name == 'zhang') { <span style="color: #008000;">//</span><span style="color: #008000;">获取name='zhang'的那条数据</span>
        <span style="color: #0000ff;">var</span> del = you.result.<span style="color: #0000ff;">delete</span><span style="color: #000000;">();
        del.onsuccess </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
            console.log(</span>"删除成功"<span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
