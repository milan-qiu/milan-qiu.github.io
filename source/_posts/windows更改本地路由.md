---
title: "windows更改本地路由"
date: "2020-04-18 15:25:00"
updated: "2021-02-02 09:31:00"
tags:
categories:
description: >-
  1、修改本地路由表：C:\Windows\System32\drivers\etc 里面的hosts文件。 127.0.0.1 www.qml.com 2、apacha扩展配置文件打开： D:\phpStudy\PHPTutorial\Apache\conf 里面的 httpd.conf 文件 大概
---

<h3><span style="font-size: 14px;">1、修改本地路由表：C:\Windows\System32\drivers\etc&nbsp; &nbsp;里面的hosts文件。</span></h3>
<p>127.0.0.1&nbsp; &nbsp; &nbsp; &nbsp; www.qml.com</p>
<p>&nbsp;</p>
<p>2、apacha扩展配置文件打开：&nbsp; D:\phpStudy\PHPTutorial\Apache\conf&nbsp; &nbsp;里面的&nbsp; httpd.conf&nbsp; 文件</p>
<p>大概470行打开&nbsp; &nbsp; Include conf/extra/httpd-vhosts.conf</p>
<p>&nbsp;</p>
<p>3、修改apacha虚拟主机：&nbsp; D:\phpStudy\PHPTutorial\Apache\conf\extra&nbsp; &nbsp;里面的&nbsp; httpd-vhosts.conf&nbsp; 文件</p>
<p>&lt;VirtualHost *:80&gt;<br />DocumentRoot &ldquo;D:\phpStudy\PHPTutorial\WWW\xiangmu\public&rdquo;<br />ServerName www.qml.com<br />&lt;/VirtualHost&gt;</p>
<p>注：配置完虚拟主机后，就不能通过localhost进行访问了。</p>
<p>注：当执行某些控制台的操作权限不够时，可以进入C:\Windows\System32&nbsp; 找到cmd.exe，右击用管理员身份打开即可。</p>
