---
title: "1、安装Voyager"
date: "2021-02-20 17:00:00"
updated: "2021-02-20 17:35:00"
tags:
categories:
description: >-
  1、安装新项目 laravel new blog 2、进入项目下载Voyager安装包 composer require tcg/voyager 3、配置数据库信息 4、.env配置基础url APP_URL=http://myvoyager.com:8000 5、使用mysql8.0以上，或者Ap
---

<p>1、安装新项目</p>
<p>laravel new blog</p>
<p>&nbsp;</p>
<p>2、进入项目下载Voyager安装包</p>
<p>composer require tcg/voyager</p>
<p>&nbsp;</p>
<p>3、配置数据库信息</p>
<p>&nbsp;</p>
<p>4、.env配置基础url</p>
<div>APP_URL=http://myvoyager.com:8000</div>
<div>&nbsp;</div>
<div>5、使用mysql8.0以上，或者App/Providers/AppServiceProvider.php</div>
<div>先引入
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">use</span> Illuminate\Support\Facades\Schema;</pre>
</div>
</div>
<div>
<div>后在boot里面
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">function</span><span style="color: #000000;"> boot()
    {
        Schema</span>::defaultStringLength(191<span style="color: #000000;">);
    }</span></pre>
</div>
<p>&nbsp;</p>
</div>
<div>6、使用voyager迁移前，需要更改字符集，及引擎</div>
<div><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210220162312175-996724429.png" alt="" width="417" height="329" loading="lazy" />
<p>&nbsp;</p>
<p>7、php.ini开启插件支持</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210220162405904-1532657275.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;10、修改中文，在config目录下，app.php</p>
<div class="cnblogs_code">
<pre>timezone 改为 'PRC'<span>

locale 改为 'zh_CN'</span></pre>
</div>
<p>&nbsp;</p>
</div>
<div>8、先设置中文，然后再安装，开始安装Voyager
<div class="cnblogs_code">
<pre>php artisan voyager:install</pre>
</div>
<p>&nbsp;</p>
<p>9、添加管理员</p>
<div class="cnblogs_code">
<pre>php artisan voyager:admin your@email.com --create</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
</div>
<div><br />
<p>11、界面中文化，打开后台后选择Tools，选择admin，选择Menu Builder，选择某个菜单进行中文修改</p>
<p>&nbsp;</p>
</div>
</div>
