---
title: "06-JS DOM操作"
date: "2020-01-22 14:25:00"
updated: "2020-03-31 16:28:00"
tags:
categories:
description: >-
  创建节点 document.write（创建任意内容，并写入） document.write('<h1>添加到html中的文本</h1>'); docement.createElement（创建元素） var jd = document.createElement('li'); //创建一个li元素
---

<h2><span style="font-family: 幼圆;">&nbsp;</span></h2>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">创建节点</span></strong></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">document.write（创建任意内容，并写入）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">document.write('&lt;h1&gt;添加到html中的文本&lt;/h1&gt;');</span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">docement.createElement（创建元素）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #0000ff;">var</span> jd = document.createElement('li'); <span style="color: #008000;">//</span><span style="color: #008000;">创建一个li元素</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">document.createTextNode（创建文本）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #0000ff;">var</span> wb = document.createTextNode('创建的文本');  <span style="color: #008000;">//</span><span style="color: #008000;">创建一个文本内容</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">document.createDocumentFragment （创建虚拟节点对象）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #0000ff;">var</span> fragment = document.createDocumentFragment();   <span style="color: #008000;">//</span><span style="color: #008000;">创建一虚拟的节点对象，节点对象包含所有属性和方法。</span>
<span style="color: #000000;">
//document.createDocumentFragment()优点：说白了就是为了节约使用DOM。每隔JavaScript对DOM的操作都会改变页面的变现，并重新刷新整个页面，从而减少消耗的时间。为解决这个问题，可以创建一个文档碎片，把所有的新摘要附加其上，然后把文档碎片的内容一次性添加到文档中。</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">&nbsp;document.createComment（创建注释）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #0000ff;">var</span> zhuxi = document.createComment('注释的内容');  <span style="color: #008000;">//</span><span style="color: #008000;">创建一个注释内容</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-size: 16px;"><span style="font-family: 幼圆;">&nbsp;注：以上创建的节点需要&nbsp; xx.appendChild()的方法添加到页面中。document.write除外。</span></span></p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">高效创建节点</span></strong></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">innerHTML</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #000000;">innerHTML：用来设置或获取当前标签的起始和结束里面的内容

html文档：</span>&lt;div id='dd' &gt;&lt;p&gt; 321&lt;p&gt; &lt;/div&gt;
<span style="color: #000000;">
script文档1：  </span><span style="color: #008000;">//</span><span style="color: #008000;">设置</span>

<span style="color: #0000ff;">var</span> dd = document.getElementById('dd'<span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> str = '&lt;p&gt;文本1&lt;/p&gt;'
+'&lt;h1&gt;标题节点&lt;/h1&gt;'
+'&lt;h2&gt;小标题节点&lt;/h2&gt;'<span style="color: #000000;">;
dd.innerHTML </span>= str;         <span style="color: #008000;">//</span><span style="color: #008000;">原来div里面的元素都被替换</span>
<span style="color: #000000;">
script文档2：  </span><span style="color: #008000;">//</span><span style="color: #008000;">获取</span>

<span style="color: #0000ff;">var</span> dd = document.getElementById('dd'<span style="color: #000000;">);
console.log(dd.innerHTML);    </span><span style="color: #008000;">//</span><span style="color: #008000;">获取到的值为&lt;p&gt; 321&lt;p&gt;</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">&nbsp;outerHTML</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #000000;">outerHTML：返回调用它的元素及所有子节点的HTML标签

html文档：</span>&lt;div id='dd' &gt; 321 &lt;/div&gt;
<span style="color: #000000;">
script文档1：

</span><span style="color: #0000ff;">var</span> dd = document.getElementById('dd'<span style="color: #000000;">);
console.log(dd.outerHTML);    </span><span style="color: #008000;">//</span><span style="color: #008000;">返回值&lt;div id='dd' &gt; 321 &lt;/div&gt;</span>
<span style="color: #000000;">
script文档2：

</span><span style="color: #0000ff;">var</span> dd = document.getElementById('dd'<span style="color: #000000;">);
dd.outerHTML </span>= '&lt;p&gt; 清空原来的所有值，变成这个 &lt;/p&gt;';    <span style="color: #008000;">//</span><span style="color: #008000;">原来的值是321。</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">&nbsp;interText</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #000000;">interText：设置或获取位于对象起始和结束标签内的文本。

html文档：</span>&lt;div id='dd' &gt;&lt;p&gt; 321&lt;p&gt; &lt;/div&gt;
<span style="color: #000000;">
script文档： </span><span style="color: #008000;">//</span><span style="color: #008000;">获取目标文档</span>

<span style="color: #0000ff;">var</span> dd = document.getElementById('dd'<span style="color: #000000;">);
console.log(dd.innerText);          </span><span style="color: #008000;">//</span><span style="color: #008000;">打印321</span>
<span style="color: #000000;">
script文档2：   </span><span style="color: #008000;">//</span><span style="color: #008000;">设置目标文档</span>

<span style="color: #0000ff;">var</span> dd = document.getElementById('dd'<span style="color: #000000;">);
console.log(dd.innerText);
dd.innerText </span>= '&lt;p&gt; 替换原来所有的文本 &lt;/p&gt;';     <span style="color: #008000;">//</span><span style="color: #008000;">屏幕div显示，&lt;p&gt; 替换原来所有的文本 &lt;/p&gt;，p标签也会当作文档显示出来</span>
<span style="color: #000000;">
注：火狐浏览器不支持该标签，不过有类似标签textContent</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">&nbsp;outerText 与 innerText 的区别</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #000000;">outerText：获取文档跟innerText一样，设置不一样，如，

html文档：</span>&lt;div id='dd' &gt;&lt;p&gt; 321&lt;p&gt; &lt;/div&gt;
<span style="color: #000000;">
script文档：

</span><span style="color: #0000ff;">var</span> dd = document.getElementById('dd'<span style="color: #000000;">);
console.log(dd.innerText);
dd.outerText </span>= '&lt;p&gt; 替换原来所有的文本 &lt;/p&gt;';    <span style="color: #008000;">//</span><span style="color: #008000;">屏幕依然显示&lt;p&gt; 替换原来所有的文本 &lt;/p&gt;，但是原来的div已经不复存在，只留下文本    &lt;p&gt; 替换原来所有的文本 &lt;/p&gt;</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">父子节点查找</span></strong></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">父节点 找 子节点</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #000000;"> 找第一个子节点：firstChild<br />
找最后一个子节点：lastChild<br />
  找第n个子节点：childNodes[n</span>-1]　　<span style="color: #008000;">//</span><span style="color: #008000;">从0开始算<br /></span>
<span style="color: #000000;">  找第n个子节点：childNodes.item(n</span>-1)　　<span style="color: #008000;">//</span><span style="color: #008000;">从0开始算 </span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">子节点 找 父节点</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">找父节点：parentNode</span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">子节点 找 兄弟节点</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">找下一个兄弟节点：nextSibling</span><br /><br /><span style="font-family: 幼圆;">找上一个兄弟节点：previousSibling</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 16px;">找文档根节点</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">直接查找文档的根节点：<span style="color: #0000ff;">var</span> gen =<span style="color: #000000;"> document.documentElement;

直接查找文档的根节点：</span><span style="color: #0000ff;">var</span> gen = p.ownerDocument;      <span style="color: #008000;">//</span><span style="color: #008000;">现在gen = document</span>
<span style="color: #000000;">
tagName：返回属性的标签名。  </span><span style="color: #008000;">//</span><span style="color: #008000;">如，console.log('gen.tagName');  直接打印出根节点。</span>
<span style="color: #000000;">
元素名.hasChildNodes();   </span><span style="color: #008000;">//</span><span style="color: #008000;">判断该元素是否有子节点，返回Boolean值。包括文本节点。</span>
<span style="color: #000000;">
 

console.log(gen.children[i]); </span><span style="color: #008000;">//</span><span style="color: #008000;">打印出第 i+1 个节点，不包括文本节点，从0开始算</span>

<span style="color: #0000ff;">var</span> shu =  gen.childElementCount;  <span style="color: #008000;">//</span><span style="color: #008000;">算出有多少个非文本节点的节点</span></span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">类数组对象</span></strong></p>
<p><span style="font-family: 幼圆;"><strong>类数组对象NodeList，转换成数组，再添加一个节点。</strong></span></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/1680452/202003/1680452-20200331161642268-731013282.png" alt="" /></p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆;"><strong>HTMLCollection（获取类数组对象）</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #0000ff;">var</span> script = document.scripts;  <span style="color: #008000;">//</span><span style="color: #008000;">获取当前html里面所有的script</span>

<span style="color: #0000ff;">var</span> links = document.links;  <span style="color: #008000;">//</span><span style="color: #008000;">返回当前html中所有的a标签链接</span>

<span style="color: #0000ff;">var</span> cells = document.getElementById('tr').cells;  <span style="color: #008000;">//</span><span style="color: #008000;">获取当前html中，所有的td元素</span>

<span style="color: #0000ff;">var</span> imgs = document.images;  <span style="color: #008000;">//</span><span style="color: #008000;">获取当前html中，所有的图片</span>

<span style="color: #0000ff;">var</span> forms = document.forms;  <span style="color: #008000;">//</span><span style="color: #008000;">获取当前html中，所有的表单</span>

<span style="color: #0000ff;">var</span> options = document.getElementById('select').options;  <span style="color: #008000;">//</span><span style="color: #008000;">获取当前html中，所有的option选项</span>

<span style="color: #0000ff;">var</span> ps = document.getElementsByTagName('p');  <span style="color: #008000;">//</span><span style="color: #008000;">获取当前html中，的所有p标签的内容</span>
<span style="color: #000000;">
以上的值返回的都是HTMCollection</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;">类数组对象<strong>NameNodeMap</strong></span></p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202003/1680452-20200331161707683-223337669.png" alt="" /></p>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>类数组对象的动态性</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Nodelist，HTMLcollection, NamedNodeMap 三个集合都是 <strong>动态的, 是有生命、有呼吸的对象</strong>

它们实际上是基于DOM结构动态执行查询的结果,因此<strong>DOM结构的变化能够自动反映这些对象中</strong>

每当文档结构发生变化时,它们都会得到更新。因此,<strong>它们始终都会保存着最新、最准确的信息</strong></span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">获取节点</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">IE6 到 IE8 也兼容</span><br /><span style="font-family: 幼圆;">getElementById()</span><br /><span style="font-family: 幼圆;">getElementsByName()</span><br /><span style="font-family: 幼圆;">getElementsByTagName()</span><br /><br /><span style="font-family: 幼圆;">IE9 或以上</span><br /><span style="font-family: 幼圆;">getElementsByClassName()</span><br /><span style="font-family: 幼圆;">querySelector()</span><br /><span style="font-family: 幼圆;">querySelectorAll()</span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">操作节点</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">='abc'</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span> 1 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span> 2 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span> 3 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>appendChild()&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">appendChild()  <span style="color: #008000;">//</span><span style="color: #008000;">为指定元素节点的最后一个子节点之后添加节点。该方法返回新的子节点。</span>
<span style="color: #000000;">
如：要为上面ul添加一个li

</span><span style="color: #0000ff;">var</span> abc = document.getElementById('abc');   <span style="color: #008000;">//</span><span style="color: #008000;">获取ul元素对象</span>

<span style="color: #0000ff;">var</span> text = document.creatTextNode('4');   <span style="color: #008000;">//</span><span style="color: #008000;">创建文本节点4</span>

<span style="color: #0000ff;">var</span> li = document.createElement('li');   <span style="color: #008000;">//</span><span style="color: #008000;">创建li元素</span>
<span style="color: #000000;">
li.appendChild(text);    </span><span style="color: #008000;">//</span><span style="color: #008000;">给li元素填入文本节点4</span>
<span style="color: #000000;">
ul.appendChild(li);    </span><span style="color: #008000;">//</span><span style="color: #008000;">给ul元素填入刚才的li元素</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>insertBefore()&nbsp;&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">insertBefore()  <span style="color: #008000;">//</span><span style="color: #008000;">在指定的已有节点之前插入新的子节点</span>
<span style="color: #000000;">
如：要为上面</span>&lt;li&gt;2&lt;/li&gt;前面插入一个新节点

<span style="color: #0000ff;">var</span> abc = document.getElementById('abc');   <span style="color: #008000;">//</span><span style="color: #008000;">获取ul元素对象</span>

<span style="color: #0000ff;">var</span> text = document.creatTextNode('4');   <span style="color: #008000;">//</span><span style="color: #008000;">创建文本节点4</span>

<span style="color: #0000ff;">var</span> lia = document.createElement('li');   <span style="color: #008000;">//</span><span style="color: #008000;">创建li元素</span>
<span style="color: #000000;">
lia.appendChild(text);    </span><span style="color: #008000;">//</span><span style="color: #008000;">给li元素填入文本节点4</span>

<span style="color: #0000ff;">var</span> lib = abc.children.item(1);   <span style="color: #008000;">//</span><span style="color: #008000;">获取第二个子节点</span>
<span style="color: #000000;">
abc.insertBefore(lia,lib);    </span><span style="color: #008000;">//</span><span style="color: #008000;">lia为要插入的节点，插入的位置是lib的前面，若是lib写成null，则效果跟appendChild一样。</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>replaceChild()</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">replaceChild(要插入的节点，被替换的节点)   <span style="color: #008000;">//</span><span style="color: #008000;">用新的节点替换某个子节点，返回值是被替换的子节点</span>
<span style="color: #000000;">
如：要为上面</span>&lt;li&gt;3&lt;/li&gt;替换成&lt;li&gt;4&lt;/li&gt;

<span style="color: #0000ff;">var</span> abc = document.getElementById('abc');   <span style="color: #008000;">//</span><span style="color: #008000;">获取ul元素对象</span>

<span style="color: #0000ff;">var</span> text = document.creatTextNode('4');   <span style="color: #008000;">//</span><span style="color: #008000;">创建文本节点4</span>

<span style="color: #0000ff;">var</span> lia = document.createElement('li');   <span style="color: #008000;">//</span><span style="color: #008000;">创建li元素</span>
<span style="color: #000000;">
lia.appendChild(text);    </span><span style="color: #008000;">//</span><span style="color: #008000;">给li元素填入文本节点4</span>

<span style="color: #0000ff;">var</span> lib = abc.children.item(2);   <span style="color: #008000;">//</span><span style="color: #008000;">获取第3个子节点</span>
<span style="color: #000000;">
abc.replaceChild( lia,lib );   </span><span style="color: #008000;">//</span><span style="color: #008000;">lia是要插入的节点，lib是被替换的节点。</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>cloneNode()&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">cloneNode(<span style="color: #0000ff;">true</span>/false)   //节点的拷贝，返回该副本。不填时为false，false表示只拷贝当前节点的标签元素，不拷贝子节点；true表示连同子节点一起拷贝。
<span style="color: #000000;">
如：拷贝一份ul到当前的body里面

</span><span style="color: #0000ff;">var</span> abc = document.getElementById('abc');   <span style="color: #008000;">//</span><span style="color: #008000;">获取ul元素对象</span>

<span style="color: #0000ff;">var</span> clone = abc.cloneNode(<span style="color: #0000ff;">true</span>);    <span style="color: #008000;">//</span><span style="color: #008000;">连同子节点一起拷贝</span>
<span style="color: #000000;">
document.body.appendChild(clone);     </span><span style="color: #008000;">//</span><span style="color: #008000;">拷贝的节点要有父节点，没有父节点的话得通过appendChild、insertBefore、replaceChild等方式进行添加</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>normalize()&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre>normalize()    <span style="color: #008000;">//</span><span style="color: #008000;">合并相邻的text节点</span>

<span style="color: #0000ff;">var</span> div = document.creatElement('div');   <span style="color: #008000;">//</span><span style="color: #008000;">创建一个div</span>

<span style="color: #0000ff;">var</span> text = document.creatTextNode('123');    <span style="color: #008000;">//</span><span style="color: #008000;">创建第一个文本节点</span>
<span style="color: #000000;">
div.appendChild(text);     </span><span style="color: #008000;">//</span><span style="color: #008000;">把第一个文本节点添加到div里面</span>

<span style="color: #0000ff;">var</span> text2 = document.creatTextNode('456');    <span style="color: #008000;">//</span><span style="color: #008000;">创建第二个文本节点</span>
<span style="color: #000000;">
div.appendChild(text2);    </span><span style="color: #008000;">//</span><span style="color: #008000;">把第二个文本节点添加到div里面</span>
<span style="color: #000000;">
document.body.appendChild(div);   </span><span style="color: #008000;">//</span><span style="color: #008000;">在body显示div</span></pre>
</div>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202003/1680452-20200331162713931-1071328712.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">可以看见右边调试工具的文本节点有两个的</span>
<span style="color: #000000;">
div.normalize();   </span><span style="color: #008000;">//</span><span style="color: #008000;">这样我们就能把两个节点合并为一个节点了</span></pre>
</div>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202003/1680452-20200331162741306-1596209088.png" alt="" /></p>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>splitText()&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">splitText()    <span style="color: #008000;">//</span><span style="color: #008000;">按照指定位置把一个文本节点分割为两个文本节点，返回新的文本节点</span>

<span style="color: #0000ff;">var</span> div = document.creatElement('div');   <span style="color: #008000;">//</span><span style="color: #008000;">创建一个div</span>

<span style="color: #0000ff;">var</span> text = document.creatTextNode('123456');    <span style="color: #008000;">//</span><span style="color: #008000;">创建一个文本节点</span>
<span style="color: #000000;">
div.appendChild(text);     </span><span style="color: #008000;">//</span><span style="color: #008000;">把文本节点添加到div里面</span>

<span style="color: #0000ff;">var</span> fen = div.firstChild.splitText(3);   <span style="color: #008000;">//</span><span style="color: #008000;">从第4个开始分割，包含第四个。</span>
<span style="color: #000000;">
console.log(div.firstChild.nodeValue);   </span><span style="color: #008000;">//</span><span style="color: #008000;">控制台打印出第一个文本节点，即123</span></span></pre>
</div>
<p><span style="font-family: 幼圆;">&nbsp;</span></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-family: 幼圆; font-size: 14pt;">删除节点</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;"><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">='abc'</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span> 1 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span> 2 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span> 3 <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>removeChild()&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">removeChild()   <span style="color: #008000;">//</span><span style="color: #008000;">删除某个节点，括号必须传入要删除的节点，返回删除的节点</span>
<span style="color: #000000;">
如：删除上面</span>&lt;li&gt;1&lt;/li&gt;节点

<span style="color: #0000ff;">var</span>  abc = document.getElementById('abc');   <span style="color: #008000;">//</span><span style="color: #008000;">获取ul元素id</span>

<span style="color: #0000ff;">var</span> del = abc.removeChild(abc.childNodes[1]);   <span style="color: #008000;">//</span><span style="color: #008000;">删除第二个节点，上面一共7个节点，7个节点里面包含空白节点</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>removeNode()</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">removeNode()   <span style="color: #008000;">//</span><span style="color: #008000;">ie私有，参数是布尔值，默认为false。false时只删除改节点，true时连同子节点一起删</span>
<span style="color: #000000;">
如：删除上面的ul节点，不删子节点

</span><span style="color: #0000ff;">var</span>  abc = document.getElementById('abc');   <span style="color: #008000;">//</span><span style="color: #008000;">获取ul元素id</span>

<span style="color: #0000ff;">var</span> del =<span style="color: #000000;"> abc.removeNode();

如：删除上面的ul节点，连同子节点

</span><span style="color: #0000ff;">var</span>  abc = document.getElementById('abc');   <span style="color: #008000;">//</span><span style="color: #008000;">获取ul元素id</span>

<span style="color: #0000ff;">var</span> del = abc.removeNode(<span style="color: #0000ff;">true</span>);</span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: 幼圆; font-size: 16px;"><strong>removeChild()与innerHTML的区别</strong></span></p>
<div class="cnblogs_code">
<pre><span style="font-family: 幼圆;">removeChild()，在ie6-<span style="color: #000000;">8删除后还可以调用；在chrome删除后还可以调用

innerHTML，在ie6</span>-<span style="color: #000000;">8删除后还不可以调用；在chrome删除后还可以调用

ps：调用指的是元素对应的方法，而不是元素本身</span></span></pre>
</div>
