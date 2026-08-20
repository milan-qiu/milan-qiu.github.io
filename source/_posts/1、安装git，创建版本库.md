---
title: "1、安装git，创建版本库"
date: "2020-06-27 17:37:00"
updated: "2020-06-27 18:25:00"
tags:
categories:
description: >-
  一、windows下载地址 https://git-scm.com/download/win 二、默认安装，一路回车 三、完成后配置全局用户名、邮箱（右键Git Bash Here） git config --global user.name "Mingliang" git config --glo
---

<p>一、windows下载地址</p>
<p><a href="https://git-scm.com/download/win" target="_blank">https://git-scm.com/download/win</a></p>
<p>&nbsp;</p>
<p>二、默认安装，一路回车</p>
<p>&nbsp;</p>
<p>三、完成后配置全局用户名、邮箱（右键Git Bash Here）</p>
<div class="cnblogs_code">
<pre>git config --<span style="color: #0000ff;">global</span> user.name <span style="color: #800000;">"</span><span style="color: #800000;">Mingliang</span><span style="color: #800000;">"</span><span style="color: #000000;">
git config </span>--<span style="color: #0000ff;">global</span> user.email <span style="color: #800000;">"</span><span style="color: #800000;">xiaoliang0730@163.com</span><span style="color: #800000;">"</span></pre>
</div>
<p>&nbsp;</p>
<p>四、选择创建本地存储库</p>
<div class="cnblogs_code">
<pre>git init</pre>
</div>
<p>&nbsp;</p>
<p>五、建立远程仓库</p>
<p>1、生成 SHH Key ，默认一路回车即可</p>
<div class="cnblogs_code">
<pre>ssh-keygen -t rsa -C <span style="color: #800000;">"</span><span style="color: #800000;">xiaoliang0730@163.com</span><span style="color: #800000;">"</span></pre>
</div>
<p>2、建立github远程仓库，粘贴公钥</p>
<p>3、建立gitee远程仓库，粘贴公钥</p>
<p>注：建立仓库时，先不要放README</p>
<p>&nbsp;</p>
<p>六、关联远程仓库</p>
<p>1、复制 https / ssh 链接，进行关联</p>
<div class="cnblogs_code">
<pre>git remote add origin git@gitee.com:mingliangge/mingliangge.gitee.io.git</pre>
</div>
<p>&nbsp;</p>
<p>七、尝试提交文件</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">查看当前文件是否有修改</span>
<span style="color: #000000;">git status

</span><span style="color: #008000;">//</span><span style="color: #008000;">修改了哪部分</span>
<span style="color: #000000;">git diff

</span><span style="color: #008000;">//</span><span style="color: #008000;">工作区新建文件</span>
<span style="color: #000000;">touch a.txt

</span><span style="color: #008000;">//</span><span style="color: #008000;">提交到暂存区</span>
<span style="color: #000000;">git add a.txt

</span><span style="color: #008000;">//</span><span style="color: #008000;">提交到本地仓库</span>
git commit -m <span style="color: #800000;">"</span><span style="color: #800000;">描述这次提交做了什么事</span><span style="color: #800000;">"</span>

<span style="color: #008000;">//</span><span style="color: #008000;">提交到远程仓库，第一次提交加上 -u</span>
git push -u origin master</pre>
</div>
<p>注：遇到冲突？稍后介绍</p>
<p>&nbsp;</p>
<p>六、关联远程版本库另一方法</p>
<p>1、克隆远程仓库</p>
<p>2、进行关联</p>
<p>3、尝试提交......</p>
