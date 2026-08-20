---
title: "13、Laravel中的用户认证（Auth）"
date: "2020-07-03 15:19:00"
updated: "2021-01-31 23:35:00"
tags:
categories:
description: >-
  生成Auth所需命令 一、在已有的项目中生成auth认证 composer require laravel/ui php artisan ui vue --auth npm install && npm run dev 二、新建项目，并直接生成auth认证 laravel new blog --au
---

<h2>生成Auth所需命令</h2>
<p>一、在已有的项目中生成auth认证</p>
<div class="cnblogs_code">
<pre>composer require laravel/ui&nbsp;</pre>
</div>
<div class="cnblogs_code">
<pre>php artisan ui vue --auth</pre>
</div>
<div class="cnblogs_code">
<pre>npm install &amp;&amp; npm run dev</pre>
</div>
<p>&nbsp;</p>
<p><span style="text-decoration: line-through;">二、新建项目，并直接生成auth认证</span></p>
<div class="cnblogs_code">
<pre>laravel <span style="color: #0000ff;">new</span> blog --auth</pre>
</div>
<p>&nbsp;</p>
<p>三、打开服务器后即可网页预览</p>
<p>&nbsp;</p>
<p>四、.env更改数据库配置后，新建数据表（mysql5.7以上，若不是就需要更改字段类型）</p>
<div class="cnblogs_code">
<pre>php artisan migrate</pre>
</div>
<p>&nbsp;实际执行 database -&gt; migrations -&gt; 里面的迁移表</p>
<p>更改字段类型：config -&gt; database.php -&gt; 里面的 charset 换成 utf8，里面的 collation 换成 utf8_unicode_ci（大概56-57行）</p>
<p>&nbsp;</p>
<h2>数据迁移</h2>
<p>一、第一种生成迁移文件方法</p>
<div class="cnblogs_code">
<pre>php artisan make:migration create_students_table --create=students</pre>
</div>
<p>--table 和 --create 参数可以用来指定数据表名称，以及迁移文件是否要建立新的数据表</p>
<p>&nbsp;</p>
<p>二、第二种，生成模型的同时生成迁移文件</p>
<div class="cnblogs_code">
<pre>php artisan make:model Student -m</pre>
</div>
<p>&nbsp;</p>
<p>三、执行生成操作</p>
<div class="cnblogs_code">
<pre>php artisan migrate</pre>
</div>
<p>&nbsp;</p>
<p>四、根据具体需求修改刚生成的迁移文件</p>
<div class="cnblogs_code">
<pre>//若将迁移文件里面的字段进行了更改，需要同步到数据库需要
php artisan migrate:refresh</pre>
</div>
<p>&nbsp;</p>
<p>五、回滚失误操作</p>
<div class="cnblogs_code">
<pre>php artisan migrate:rollback --step=1     <span style="color: #008000;">//</span><span style="color: #008000;">表示回滚上一次操作</span></pre>
</div>
<p>&nbsp;</p>
<p>六、删除所有数据库表，并不会删除迁移文件</p>
<div class="cnblogs_code">
<pre>php artisan migrate:<span style="color: #008080;">reset</span></pre>
</div>
<p>&nbsp;</p>
<h2>数据填充</h2>
<p>一、创建一个填充文件（最后一个参数为填充文件名）</p>
<div class="cnblogs_code">
<pre>php artisan make:seeder StudentTableSeeder</pre>
</div>
<p>&nbsp;位于database -&gt; seeds 里面的 StudentTableSeeder.php</p>
<p>&nbsp;在run里面填入插入语句</p>
<p>&nbsp;</p>
<p>二、执行单个填充文件（最后一个参数为填充文件名）</p>
<div class="cnblogs_code">
<pre>php artisan db:seed --<span style="color: #0000ff;">class</span>=StudentTableSeeder</pre>
</div>
<p>&nbsp;</p>
<p>三、批量执行填充文件</p>
<div class="cnblogs_code">
<pre>php artisan db:seed</pre>
</div>
<p>生成多个填充文件后，在&nbsp;database -&gt; seeds 里面的 DatabaseSeeder.php 的run里面进行引入多个填充文件，后执行批量填充语句</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">run函数里面</span>
<span style="color: #800080;">$this</span> -&gt; call (StudentSeeder::<span style="color: #0000ff;">class</span>);</pre>
</div>
<p>四、生成数据表的同时插入数据</p>
<div class="cnblogs_code">
<pre>php artisan migrate:refresh --seed</pre>
</div>
<p><strong>五、利用 factory 批量制造伪数据</strong></p>
<p>1、在 databade\factories 下选择某个工厂类</p>
<p>2、配置字段需要填充什么值</p>
<p>3、php artisan tinker 进入shell命令行</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">先定义命名空间</span>
<span style="color: #000000;">namespace App\Models;

</span><span style="color: #008000;">//</span><span style="color: #008000;">查看数据表原有内容</span>
<span style="color: #800080;">$users</span> = User::<span style="color: #000000;">all();

</span><span style="color: #008000;">//</span><span style="color: #008000;">选择工厂类，要插入多少条，开始执行</span>
User::factory()-&gt;<span style="color: #008080;">count</span>(10)-&gt;create();</pre>
</div>
<p>&nbsp;</p>
<p>创建一个新的factory类，并绑定某一个model</p>
<p>1、创建一个新的model类，并生成迁移文件</p>
<div class="cnblogs_code">
<pre>php artisan make:model Post -<span style="color: #000000;">m
</span><span style="color: #008000;">//</span><span style="color: #008000;">Post类带迁移文件</span></pre>
</div>
<p>&nbsp;</p>
<p>2、执行迁移文件，并填充一点数据</p>
<div class="cnblogs_code">
<pre>php artisan migrate</pre>
</div>
<div class="cnblogs_code">
<pre>php artisan db::seed</pre>
</div>
<p>&nbsp;</p>
<p>3、开始新增工厂类，并绑定model类</p>
<div class="cnblogs_code">
<pre>php artisan make:factory PostFactory -<span style="color: #000000;">m Post
</span><span style="color: #008000;">//</span><span style="color: #008000;">工厂类PostFactory绑定model类Post</span></pre>
</div>
<p>虚拟数据时，设置文章的user_id，从user表里面随机获取，写在迁移文件</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">先指定表外键</span>
<span style="color: #800080;">$table</span>-&gt;unsignedInterge(''<span style="color: #000000;">author_id);

</span><span style="color: #008000;">//</span><span style="color: #008000;">另主键id关联user表的id</span>
<span style="color: #800080;">$table</span>-&gt;foreign('author_id')-&gt;references('id')-&gt;on('users');</pre>
</div>
<p>&nbsp;</p>
