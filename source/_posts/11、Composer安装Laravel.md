---
title: "11、Composer安装Laravel"
date: "2020-07-01 22:47:00"
updated: "2021-02-02 09:22:00"
tags:
categories:
description: >-
  安装配置 composer 一、通过phpstudy下载好composer插件 二、查找 php 和 composer 的.exe目录 1、dom窗口找php目录：where php 2、dom窗口找composer目录：where composer 三、将查找到的目录添加到环境变量中。（不需要后面
---

<h2>安装配置 composer</h2>
<p>一、通过phpstudy下载好composer插件</p>
<p>&nbsp;</p>
<p>二、查找 php 和 composer 的.exe目录</p>
<p>1、dom窗口找php目录：where php</p>
<p>2、dom窗口找composer目录：where composer</p>
<p>&nbsp;</p>
<p>三、将查找到的目录添加到环境变量中。（不需要后面的文件，只是目录）</p>
<p>1、按照自己需求选择添加到 用户环境变量&nbsp; 或&nbsp; 系统环境变量</p>
<p>&nbsp;</p>
<p>四、设置国内镜像源</p>
<p>1、查看当前镜像源：composer config -gl&nbsp;</p>
<p>2、配置国内镜像源：<code class="lang-bash">composer config -g repo.packagist composer https://packagist.phpcomposer.com</code></p>
<p>&nbsp;</p>
<p>五、使用composer</p>
<p>1、搜索是否存在该软件包：composer search monolog</p>
<p>2、查看该软件包所有版本：composer show --all monolog/monolog</p>
<p>3、初始化：composer init</p>
<p>4、安装软件：</p>
<p>在composer.json里面填写包名跟版本号，如</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ming/liang</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">authors</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
        {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Mingliang</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">email</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">xiaoliang0730@163.com</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
    ],
    </span><span style="color: #800000;">"</span><span style="color: #800000;">require</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">monolog/monolog</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2.1.*</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>保存后，composer install&nbsp; 安装软件</p>
<p>&nbsp;</p>
<p>5、删除软件：</p>
<p>在composer.json里面删除对应的包，</p>
<p>保存后，composer update&nbsp; 即可删除</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>安装 Laravel&nbsp;</h2>
<p>一、第一种方法，直接在目录安装laravel包，最后一个参数为项目名</p>
<div class="cnblogs_code">
<pre>composer create-project --prefer-dist laravel/laravel lademo</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>二、第二种方法：</p>
<p>先安装laravel安装器</p>
<div class="cnblogs_code">
<pre>composer <span style="color: #0000ff;">global</span> require <span style="color: #800000;">"</span><span style="color: #800000;">laravel/installer</span><span style="color: #800000;">"</span></pre>
</div>
<p>&nbsp;</p>
<p>确保将 Composer 的全局 vendor bin 目录放置在你的系统环境变量 $PATH 中，以便系统可以找到 Laravel 的可执行文件。在不同的操作系统中，该目录的路径也不相同；下面列出一些常见的位置：</p>
<div class="cnblogs_code">
<pre>macOS: 
<span style="color: #800080;">$HOME</span>/.composer/vendor/<span style="color: #000000;">bin

Windows</span>: 
%USERPROFILE%<span style="color: #000000;">\AppData\Roaming\Composer\vendor\bin

GNU </span>/ Linux 发行版: 
<span style="color: #800080;">$HOME</span>/.config/composer/vendor/<span style="color: #000000;">bin 
或者 
</span><span style="color: #800080;">$HOME</span>/.composer/vendor/bin</pre>
</div>
<p>您也可以通过运行 composer global about 命令查找并查看 Composer 的全局安装路径</p>
<p>&nbsp;</p>
<p>创建项目，最后一个为项目名</p>
<div class="cnblogs_code">
<pre>laravel <span style="color: #0000ff;">new</span> blog</pre>
</div>
<p>&nbsp;</p>
<p>三、通过artisan 或 开启本地服务器 进行项目访问</p>
