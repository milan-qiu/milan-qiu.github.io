---
title: "1、docker安装"
date: "2021-12-05 22:25:00"
updated: "2021-12-07 12:50:00"
tags:
categories:
description: >-
  windows管理员身份运行 PowerShell Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All 下载 windows docker 并安装 https://hub.docker.com/ 测试是否
---

<p>windows管理员身份运行 PowerShell</p>
<div class="cnblogs_code">
<pre>Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All</pre>
</div>
<p>&nbsp;</p>
<p>下载 windows docker 并安装</p>
<p><a href="https://hub.docker.com/" target="_blank">https://hub.docker.com/</a></p>
<p>&nbsp;</p>
<p>测试是否安装成功</p>
<div class="cnblogs_code">
<pre>docker --version</pre>
</div>
<p>&nbsp;</p>
<p>若出现 WSL 2 installation is incomplete</p>
<p>下载安装：<a href="https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi" target="_blank">https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi</a></p>
