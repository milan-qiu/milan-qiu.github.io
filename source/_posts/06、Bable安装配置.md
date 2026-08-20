---
title: "06、Bable安装配置"
date: "2020-05-06 15:36:00"
tags:
categories:
description: >-
  Bable Bable是JavaScript的编译器 把浏览器不支持的ES6新特性，变成浏览器可执行的代码 中文官网：https://www.babeljs.cn/ 使用：可在线使用，可本地安装 本地安装 1、首先需要node.js环境 2、进入开发的项目目录，初始化 package.json： n
---

<h2>Bable</h2>
<p>Bable是JavaScript的编译器</p>
<p>把浏览器不支持的ES6新特性，变成浏览器可执行的代码</p>
<p>中文官网：<a href="https://www.babeljs.cn/">https://www.babeljs.cn/</a></p>
<p>使用：可在线使用，可本地安装</p>
<h3>本地安装</h3>
<p>1、首先需要node.js环境</p>
<p>2、进入开发的项目目录，初始化&nbsp; package.json：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">npm init
</span><span style="color: #008000;">//</span><span style="color: #008000;">后面根据需求填写，或一路回车即可</span><span style="color: #008000;">
//</span><span style="color: #008000;">或者直接使用默认的初始化</span>
npm init -y</pre>
</div>
<p>&nbsp;</p>
<p>3、安装bable，同样需要在该目录下进行</p>
<div class="cnblogs_code">
<pre>//逐个项目安装（官网新版写法）<br />npm install --save-dev @babel/core @babel/cli<br /><br />//逐个项目安装（旧版写法）<br />npm install --save-dev babel-cli<br />//简写是<br />npm i -D babel-cli</pre>
</div>
<p>//若安装失败可能权限不够，可以<br />    mac用户：sudo npm install ...<br />windows用户：用管理员打开cmd即可</p>
<p>&nbsp;</p>
<p>&nbsp;4、在package.json文件下可以看到</p>
<div class="cnblogs_code">
<pre>"dependencise"下面的包 和 "devDependencise" 下面的包都是项目开发中用到的，上线的时候这些包都不需要的</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;5、在package.json中，"scripts" 下添加</p>
<div class="cnblogs_code">
<pre>"build":"babel entry.js -o index.js -w"
<span style="color: #008000;">//</span><span style="color: #008000;">注意与上一句之间需要添加一个逗号<br />//-o index.js 表示将entry.js输出为一个新文件index.js<br />//-w 表示实时监听 entry.js ,当entry.js发生改变时，自动编译生成文件</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;6、在项目目录下创建 entry.js 文件</p>
<p>&nbsp;</p>
<p><span style="text-decoration: line-through;">&nbsp;7、写完 entry.js 后，尝试运行。这步可以忽略</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">npm run build
</span><span style="color: #008000;">//</span><span style="color: #008000;">实际上就是运行babel entry.js ，即刚才在scripts那里写的代码<br />//全局安装的时候才能直接使用 bable entry.js</span></pre>
</div>
<p>&nbsp;</p>
<h3>制定转换规则</h3>
<p>1、安装 babel-preset-env</p>
<div class="cnblogs_code">
<pre>npm i -D babel-preset-env</pre>
</div>
<p>&nbsp;</p>
<p>2、在项目中创建&nbsp;<code>.babelrc 文件</code></p>
<p>3、在 .babelrc 中制定规则</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">//新版写法<br />{
  </span>"presets": ["@babel/preset-env"<span style="color: #000000;">]
}<br />//旧版写法<br />{<br />　　"presets":[<br />　　　　"env"<br />　　]<br />}</span></pre>
</div>
<p>&nbsp;//还可以有更详细的制定计划：<a href="https://github.com/browserslist/browserslist">https://github.com/browserslist/browserslist</a></p>
<p>&nbsp;</p>
<p>4、后直接使用，会自动监听，并生成文件了</p>
<div class="cnblogs_code">
<pre>npm run build</pre>
</div>
<p>&nbsp;</p>
