---
title: "16、依赖管理 go mod 使用"
date: "2021-11-25 23:14:00"
tags:
categories:
description: >-
  尝试安装 zap 包 go get -u go.uber.org/zap go.mod 文件自动生成依赖目录 module gomodTest go 1.17 require ( go.uber.org/atomic v1.9.0 // indirect go.uber.org/multierr v
---

<p>尝试安装 <a href="https://github.com/uber-go/zap" target="_blank">zap</a> 包</p>
<div class="cnblogs_code">
<pre>go <span style="color: #0000ff;">get</span> -u go.uber.org/zap</pre>
</div>
<p>&nbsp;</p>
<p>go.mod 文件自动生成依赖目录</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">module gomodTest

go </span><span style="color: #800080;">1.17</span><span style="color: #000000;">

require (
    go.uber.org</span>/atomic v1.<span style="color: #800080;">9.0</span> <span style="color: #008000;">//</span><span style="color: #008000;"> indirect</span>
    go.uber.org/multierr v1.<span style="color: #800080;">7.0</span> <span style="color: #008000;">//</span><span style="color: #008000;"> indirect</span>
    go.uber.org/zap v1.<span style="color: #800080;">19.1</span> <span style="color: #008000;">//</span><span style="color: #008000;"> indirect</span>
)</pre>
</div>
<p>&nbsp;</p>
<p>go.mod 目录下 生成 go.sum 校验文件</p>
<p>&nbsp;</p>
<p>下载的依赖放在了go安装的位置&nbsp; &nbsp;D:\go\bin\pkg\mod\</p>
<p>&nbsp;</p>
<p>指定 依赖的版本安装</p>
<div class="cnblogs_code">
<pre>go <span style="color: #0000ff;">get</span> -u go.uber.org/zap@v1.<span style="color: #800080;">11</span></pre>
</div>
<p>&nbsp;</p>
<p>清除 .sum 文件对历史包的引用</p>
<div class="cnblogs_code">
<pre>go mod tidy</pre>
</div>
<p>&nbsp;</p>
