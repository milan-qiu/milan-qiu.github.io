---
title: "Sublime Text3"
date: "2020-04-04 15:04:00"
updated: "2020-04-04 15:11:00"
tags:
categories:
description: >-
  下载解压打开 地址：https://download.sublimetext.com/Sublime%20Text%20Build%203211%20x64.zip 安装package control ctrl + ` 后粘贴如下代码 import urllib.request,os; pf = '
---

<h2>下载解压打开</h2>
<p>地址：<a href="https://download.sublimetext.com/Sublime%20Text%20Build%203211%20x64.zip" target="_blank">https://download.sublimetext.com/Sublime%20Text%20Build%203211%20x64.zip</a></p>
<p>&nbsp;</p>
<h2>安装package control</h2>
<p>ctrl + ` 后粘贴如下代码</p>
<div class="cnblogs_code">
<pre>import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())</pre>
</div>
<p>回车，安装完后重启subline。（进度条在左下角）</p>
<p>Perferences -&gt; package settings&nbsp; 中是否有&nbsp; package control&nbsp; 这一项，如果有，则安装成功</p>
<p>&nbsp;</p>
<h2>设置中文</h2>
<h3>安装插件：</h3>
<p>Perferences&nbsp; -&gt;&nbsp; package control&nbsp; 或者 ctrl + shit + p&nbsp; ，输入install后，选择Package Control:Install Package，回车</p>
<h3>ChineseLocalizations插件</h3>
<p>搜索chinese，选择ChineseLocalizations</p>
<p>安装完成后自动变成中文，若需要换回英文：帮助&nbsp; -&gt;&nbsp; Language&nbsp; -&gt;&nbsp; English</p>
<p>&nbsp;</p>
<h2>查看已安装插件&nbsp;</h2>
<p>ctrl + shit + p 后，输入list，选择Packge Control: List Packges</p>
<p>&nbsp;</p>
<h2>删除插件</h2>
<p>ctrl + shit + p 后，输入remove，选择Packge Control: Remove Packge后，选择需要删除的插件</p>
<p>&nbsp;</p>
<h2>更新插件</h2>
<p>ctrl + shit + p 后，输入upgrade，选择Packge Control: Upgrade Packge 后自动更新，进度条在左下角</p>
<p>&nbsp;</p>
<h2>Sass</h2>
<h3>Sass Build</h3>
<p>作用：编译sass文件</p>
<p>安装完成后，工具 -&gt; 编译系统 -&gt; SASS</p>
<p>.scss 文件，ctrl+s保存后，ctrl+b编译，这时会在相同目录下，生成相同名字的.css 文件，还有同名的.css.map 文件。</p>
<p>注意：工具 -&gt; 编译系统 -&gt; SASS - Compressed ,那么生成的代码就是压缩的.css 文件。</p>
<p>&nbsp;</p>
<h3>SublimeOnSaveBuild</h3>
<p>作用：按ctrl+s 就相当于：ctrl+s 和 ctrl+b</p>
<p>安装完成后，不需要配置，编写完.scss 文件，ctrl+s 即可完成所需操作</p>
<p>&nbsp;</p>
