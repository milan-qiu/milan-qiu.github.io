---
title: "2、Voyager基本操作"
date: "2021-02-20 17:34:00"
updated: "2021-02-22 18:35:00"
tags:
categories:
description: >-
  1、利用Tools里面database进行表的创建与删除 2、关联表前，先建立BREAD，然后才能关联 3、slect dropdown 下拉菜单型（单选按钮） { "default" : "radio1", "options" : { "radio1": "Radio Button 1 Text"
---

<p>1、利用Tools里面database进行表的创建与删除</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210220171306980-1451289949.png" alt="" width="1158" height="318" loading="lazy" /></p>
<p>&nbsp;2、关联表前，先建立BREAD，然后才能关联</p>
<p>&nbsp;</p>
<h3>3、slect dropdown 下拉菜单型（单选按钮）</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span>"default" : "radio1",
    "options" :<span style="color: #000000;"> {
        </span>"radio1": "Radio Button 1 Text",
        "radio2": "Radio Button 2 Text"<span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>若是选项少也可以radio button</p>
<p>&nbsp;</p>
<p>4、添加bread时记得选择输入方式，不然在bread进行输入数据</p>
<p>&nbsp;</p>
<h3>5、图片输入函数改为</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span>"resize":<span style="color: #000000;"> {
        </span>"width": "1000",
        "height": <span style="color: #0000ff;">null</span><span style="color: #000000;">
    }</span>,
    "quality" : "70%",
    "upsize" : <span style="color: #0000ff;">true</span>,
    "thumbnails":<span style="color: #000000;"> [
        {
            </span>"name": "medium",
            "scale": "50%"<span style="color: #000000;">
        }</span>,<span style="color: #000000;">
        {
            </span>"name": "small",
            "scale": "25%"<span style="color: #000000;">
        }</span>,<span style="color: #000000;">
        {
            </span>"name": "cropped",
            "crop":<span style="color: #000000;"> {
                </span>"width": "300",
                "height": "250"<span style="color: #000000;">
            }
        }
    ]
}</span></pre>
</div>
<p>&nbsp;</p>
<p>即上传时会出现4种不同尺寸的图片，原始、中等、缩小、裁剪</p>
<p>&nbsp;</p>
<p>项目中使用略缩图等，在图片的模型（官方文档：助手模型）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">use</span><span style="color: #000000;"> TCG\Voyager\Traits\Resizable;

</span><span style="color: #0000ff;">class</span> Post <span style="color: #0000ff;">extends</span><span style="color: #000000;"> Model
{
    </span><span style="color: #0000ff;">use</span><span style="color: #000000;"> Resizable;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>在视图使用。可以指定可选的图像字段名（属性），默认为<code>image</code></p>
<div class="cnblogs_code">
<pre>@<span style="color: #0000ff;">foreach</span>(<span style="color: #800080;">$posts</span> <span style="color: #0000ff;">as</span> <span style="color: #800080;">$post</span><span style="color: #000000;">)
    </span>&lt;img src="{{Voyager::image(<span style="color: #800080;">$post</span>-&gt;thumbnail('small'))}}" /&gt;<span style="color: #000000;">
@</span><span style="color: #0000ff;">endforeach</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>6、多图像选择器使用</h3>
<p>bread输入方式改为multiple images</p>
<p>&nbsp;</p>
<h3>7、文件选择</h3>
<p>bread输入方式改为multiple images</p>
<p>若选择的文件比较多，字段必须改为text型</p>
<p>&nbsp;</p>
<p>media picker就是选择媒体库的文件</p>
<p>若expanded为true，则编辑时会自动打开媒体库选择</p>
<p>&nbsp;</p>
<h3>8、过滤显示</h3>
<p>model写对应函数</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">function</span> scopeDraft(<span style="color: #800080;">$query</span><span style="color: #000000;">){
        </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">$query</span>-&gt;where('status',1<span style="color: #000000;">);
    }</span></pre>
</div>
<p>&nbsp;</p>
<p>bread&nbsp; -&gt;&nbsp; scope&nbsp; 选择完对应函数后，就会过滤显示</p>
<p>&nbsp;</p>
<p>9、关于安全问题，修改后台路由admin为其他。</p>
<p>&nbsp;</p>
<p>10、添加统计控件，voyager配置文件添加user控件</p>
<div class="cnblogs_code">
<pre>        'widgets' =&gt;<span style="color: #000000;"> [
            \TCG\Voyager\Widgets\UserDimmer</span>::<span style="color: #0000ff;">class</span><span style="color: #000000;">
        ]</span>,</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>11、复写users视图文件（解决users表新增字段不能修改问题）</p>
<p>先在resources -&gt; views&nbsp; &nbsp;建立文件夹&nbsp; &nbsp;vendor/voyager/users</p>
<p>建立edit-add.blade.php视图文件</p>
<p>&nbsp;</p>
<p>12、bread慢的原因是引用了google的东西</p>
<p>全局搜索</p>
<div>https://ajax.googleapis.com/ajax/libs/jqueryui/1.12.0/themes/smoothness/jquery-ui.css</div>
<div>或</div>
<div>
<div>https://ajax.googleapis.com/ajax/libs/jqueryui/1.12.0/jquery-ui.min.js</div>
<div>将这两个链接</div>
</div>
<p>改为<a href="https://www.bootcdn.cn/jqueryui/1.12.0/" target="_blank">https://www.bootcdn.cn/jqueryui/1.12.0/</a>里面的链接</p>
<p>&nbsp;</p>
