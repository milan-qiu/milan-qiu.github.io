---
title: "16、laravel8 + inertia + vue3"
date: "2021-04-08 23:12:00"
tags:
categories:
description: >-
  辅助脚手架系统：https://jetstream.laravel.com/2.x/introduction.html inertia：https://inertiajs.com/ 1、安装新项目 laravel new project 1.1、更改中文模式 1.2、配置数据库信息 2、安装脚手架系
---

<p>辅助脚手架系统：<a href="https://jetstream.laravel.com/2.x/introduction.html" target="_blank">https://jetstream.laravel.com/2.x/introduction.html</a></p>
<p>inertia：<a href="https://inertiajs.com/" target="_blank">https://inertiajs.com/</a></p>
<p>&nbsp;</p>
<p>1、安装新项目</p>
<div class="cnblogs_code">
<pre>laravel <span style="color: #0000ff;">new</span> project</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>1.1、更改中文模式&nbsp;</p>
<p>&nbsp;</p>
<p>1.2、配置数据库信息</p>
<p>&nbsp;</p>
<p>2、安装脚手架系统</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">cd project
composer require laravel</span>/jetstream</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3、安装inertia</p>
<div class="cnblogs_code">
<pre>php artisan jetstream:install inertia</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>4、安装依赖</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">npm install
npm run dev
php artisan migrate</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>5、运行查看</p>
<div class="cnblogs_code">
<pre>php artisan serve&nbsp;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;npm仓库用：<a href="https://registry.npmjs.org/" target="_blank">https://registry.npmjs.org/</a></p>
<p>&nbsp;</p>
