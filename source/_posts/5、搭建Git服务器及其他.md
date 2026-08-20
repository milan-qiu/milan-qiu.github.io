---
title: "5、搭建Git服务器及其他"
date: "2020-06-28 17:51:00"
tags:
categories:
description: >-
  忽略特殊文件 一、创建 .gitignore 文件，里面写文件名或正则，如： batabase.php *.ini 二、将 .gitignore 上传到远程 三、将文件强制推送到远程 git add -f database.php 四、检查 .gittignore 语法错误 git check-ig
---

<h2>忽略特殊文件</h2>
<p>一、创建 .gitignore 文件，里面写文件名或正则，如：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">batabase.php
*.ini</span></pre>
</div>
<p>&nbsp;</p>
<p>二、将 .gitignore 上传到远程</p>
<p>&nbsp;</p>
<p>三、将文件强制推送到远程</p>
<div class="cnblogs_code">
<pre>git add -f database.php</pre>
</div>
<p>&nbsp;</p>
<p>四、检查 .gittignore 语法错误</p>
<div class="cnblogs_code">
<pre>git check-ignore -v database.php</pre>
</div>
<p>&nbsp;</p>
<h2>给命令添加别名</h2>
<p>一、用st代表status</p>
<div class="cnblogs_code">
<pre>git config --<span style="color: #0000ff;">global</span> alias.st status</pre>
</div>
<p>其他同理</p>
<p>&nbsp;</p>
<p>二、删除别名，在 .git/config 删除 [alias] 后面对应的行即可</p>
<p>&nbsp;</p>
<h2>搭建Git服务器</h2>
<p>略</p>
