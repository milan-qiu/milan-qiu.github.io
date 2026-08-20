---
title: "Axios"
date: "2020-06-03 21:30:00"
tags:
categories:
description: >-
  一、卸载vue2.0版本 npm uninstall -g vue-cli 二、安装vue3.0版本 npm install -g @vue/cli 三、查看vue版本 vue -V 四、搭建脚手架 npm create aaa 五、根据需求创建脚手架 1、选择最后一个，自定义脚手架 2、use h
---

<p>一、卸载vue2.0版本</p>
<div class="cnblogs_code">
<pre>npm uninstall -g vue-cli</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>二、安装vue3.0版本</p>
<div class="cnblogs_code">
<pre>npm install -g @vue/cli</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>三、查看vue版本</p>
<div class="cnblogs_code">
<pre>vue -V</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>四、搭建脚手架</p>
<div class="cnblogs_code">
<pre>npm create aaa</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>五、根据需求创建脚手架</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">1</span><span style="color: #000000;">、选择最后一个，自定义脚手架
</span><span style="color: #800080;">2</span><span style="color: #000000;">、use history...，选择yes
</span><span style="color: #800080;">3</span><span style="color: #000000;">、选择预编译的css预处理器
</span><span style="color: #800080;">4</span><span style="color: #000000;">、选择第一个，出现错误才报
</span><span style="color: #800080;">5</span><span style="color: #000000;">、什么时候选择eslint，保存的时候（检查语法错误）
</span><span style="color: #800080;">6</span><span style="color: #000000;">、选择In dedicated...
</span><span style="color: #800080;">7</span>、是否选择保存该配置，下次直接使用</pre>
</div>
<p>&nbsp;</p>
<p>过程中git提示，选择是。将node_modues添加到gitignore</p>
<p>&nbsp;</p>
<h2>重点</h2>
<p>一、安装axios</p>
<div class="cnblogs_code">
<pre>npm install axios -S</pre>
</div>
<p>&nbsp;</p>
<p>在package.json查看是否安装成功</p>
<p>&nbsp;</p>
<p>二、跑项目</p>
<div class="cnblogs_code">
<pre>npm run serve</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>二、停止项目，更改 views/Home.vue</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">1</span><span style="color: #000000;">、引入axios
import axios </span><span style="color: #0000ff;">from</span> <span style="color: #800000;">'</span><span style="color: #800000;">axios</span><span style="color: #800000;">'</span>

<span style="color: #800080;">2</span><span style="color: #000000;">、在components下面创建生命周期函数created
created(){
  axios.</span><span style="color: #0000ff;">get</span>(<span style="color: #800000;">'/data.json'</span><span style="color: #000000;">)   </span>/*相对于public里面的index.html而言*/<br /><span>.then((res)=&gt;{<br />console.log(res);  /*成功执行*/<br /></span><em id="__mceDel"><span>})    </span></em></pre>
<pre><em id="__mceDel"><em id="__mceDel"><span style="color: #000000;">},</span></em></em></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>三、测试：</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">1</span><span style="color: #000000;">、public里面新建data.json
{
  </span><span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span> : <span style="color: #800000;">'</span><span style="color: #800000;">zhangsan</span><span style="color: #800000;">'</span><span style="color: #000000;">,
  </span><span style="color: #800000;">'</span><span style="color: #800000;">age</span><span style="color: #800000;">'</span> : <span style="color: #800000;">'</span><span style="color: #800000;">16</span><span style="color: #800000;">'</span><span style="color: #000000;">    
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>四、测试</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">1</span><span style="color: #000000;">、打开localhost后，查看控制台，会输出获取到的数据
</span><span style="color: #800080;">2</span>、可以在network里面找到data.json</pre>
</div>
<p>&nbsp;</p>
