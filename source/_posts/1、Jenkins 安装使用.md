---
title: "1、Jenkins 安装使用"
date: "2022-02-18 12:35:00"
updated: "2022-02-22 19:15:00"
tags:
categories:
description: >-
  安装 安装稳定版 docker pull jenkins/jenkins:lts 创建jenkin挂载目录 mkdir -p /d/jenkins_home 创建容器挂载并运行 docker run -d --name jenkins -p 8080:8080 -v /d/jenkins_home:
---

<h2>安装</h2>
<p>安装稳定版</p>
<div class="cnblogs_code">
<pre>docker pull jenkins/jenkins:lts</pre>
</div>
<p>&nbsp;</p>
<p>创建jenkin挂载目录</p>
<div class="cnblogs_code">
<pre>mkdir  -p /d/jenkins_home</pre>
</div>
<p>&nbsp;</p>
<p>创建容器挂载并运行</p>
<div class="cnblogs_code">
<pre>docker run -d --name jenkins -p <span style="color: #800080;">8080</span>:<span style="color: #800080;">8080</span> -v /d/jenkins_home:/<span style="color: #0000ff;">var</span>/jenkins_home jenkins/jenkins:lts</pre>
</div>
<p>&nbsp;</p>
<p>查看运行情况</p>
<div class="cnblogs_code">
<pre>docker ps | grep jenkins</pre>
</div>
<p>&nbsp;</p>
<p>访问jenkins</p>
<p><a href="http://localhost:8080" target="_blank"><code class="hljs awk" data-spm-anchor-id="a2c6h.12873639.0.i21.6a06b30668UL6x">http:<span class="hljs-regexp">//localhost<span class="hljs-number"><span class="hljs-number">:<span class="hljs-number">8080</span></span></span></span></code></a></p>
<p>&nbsp;</p>
<p>进入容器查看密码</p>
<div class="cnblogs_code">
<pre>docker exec -<span style="color: #000000;">it jenkins bash

cat </span>/<span style="color: #0000ff;">var</span>/jenkins_home/secrets/initialAdminPassword</pre>
</div>
<p>&nbsp;</p>
<p>选择是否安装插件</p>
<p>新建管理员用户</p>
<p>完成</p>
<p>&nbsp;</p>
<h2>使用</h2>
<p>新建自由风格的任务</p>
<p>源码管理 -&gt; Git -&gt; 配置 Repository URL</p>
<p>源码管理 -&gt; 添加Credentials</p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202202/1680452-20220218122914877-1317400412.png" alt="" width="656" height="384" loading="lazy" /></p>
<p>&nbsp;</p>
<p>后获取git私钥粘贴</p>
<div class="cnblogs_code">
<pre>cat ~/.ssh/id_rsa</pre>
</div>
<p>&nbsp;</p>
<p>构建触发器选择</p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202202/1680452-20220218123327211-1255351987.png" alt="" width="612" height="113" loading="lazy" /></p>
<p>&nbsp;</p>
<p>后项目配置webhook后进行自动化构建</p>
<p>&nbsp;</p>
<p>选择构建环境</p>
<p>输入构建命令完成</p>
<p>&nbsp;</p>
