---
title: "2、Git基本操作"
date: "2020-06-27 18:21:00"
tags:
categories:
description: >-
  一、尝试对文件进行多次修改，并提交到暂存区、本地仓库 二、基本理论 1、git add 是将文件放进暂存区，可放入多次，最后来一个git commit 2、git commit 是将暂存区的内容 提交到 当前分支 3、git status 检测你是否对当前工作区文件进行修改，且尚未提交到暂存区 4、
---

<p>一、尝试对文件进行多次修改，并提交到暂存区、本地仓库</p>
<p>&nbsp;</p>
<p>二、基本理论</p>
<p>1、git add 是将文件放进暂存区，可放入多次，最后来一个git commit</p>
<p>2、git commit 是将暂存区的内容 提交到 当前分支</p>
<p>3、git status 检测你是否对当前工作区文件进行修改，且尚未提交到暂存区</p>
<p>4、git diff 查看工作区和暂存区的差异（如：工作区新增的文件，暂存区没有，那这个命令就检测不到新的文件）</p>
<p>5、git diff HEAD 查看工作区和仓库的差异（如：git diff HEAD -- a.txt）</p>
<p>&nbsp;</p>
<p>三、工作区操作</p>
<p>1、<code class="ruby">git checkout -- a.txt （让文件回到最后一次git add 或 git commit 的状态）</code></p>
<p>&nbsp;</p>
<p>四、暂存区操作</p>
<p>1、git reset HEAD a.txt （把暂存区的修改撤销掉（unstage），重新放回工作区）</p>
<p>&nbsp;</p>
<p>五、版本库操作</p>
<p>想要回退到之前某个点？</p>
<p>1、查看想要恢复到哪个，前面一小段为commit id</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">查看commit日志</span>
<span style="color: #000000;">git log

</span><span style="color: #008000;">//</span><span style="color: #008000;">简略查看</span>
git log --pretty=oneline</pre>
</div>
<p>&nbsp;</p>
<p>2、回退上一版本</p>
<div class="cnblogs_code">
<pre>git reset --hard HEAD^</pre>
</div>
<p>注：回退到上上一版本为 git reset --hard HEAD^^ ，回退到上45个版本 git reset --hard HEAD~45</p>
<p>&nbsp;</p>
<p>3、取消回退 / 回退到某一个点</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">hard后面为commit id的一小段</span>
git reset --hard 1094a</pre>
</div>
<p>&nbsp;</p>
<p>4、第二天找不到昨天的commit id怎么回退？</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">记录了你的每一次命令</span>
git reflog</pre>
</div>
<p>&nbsp;</p>
<p>六、删除工作区文件，并同步到版本库</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">删除文件</span>
<span style="color: #000000;">git rm a.txt

</span><span style="color: #008000;">//</span><span style="color: #008000;">同步版本库</span>
git commit -m <span style="color: #800000;">"</span><span style="color: #800000;">从版本库删除了</span><span style="color: #800000;">"</span></pre>
</div>
<p>或者rm a.txt -&gt; git add a.txt -&gt; git commit -m "删除了文件"</p>
<p>&nbsp;</p>
