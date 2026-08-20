---
title: "04、PHP常用操作"
date: "2020-12-06 23:34:00"
updated: "2020-12-18 13:06:00"
tags:
categories:
description: >-
  一、文件操作 文件目录函数库 文件相关 //获取文件$file_name = "./text.txt"; //返回文件类型 echo filetype($file_name),'<br>'; //返回文件大小（字节数） echo filesize($file_name),'<br>'; //返回文件
---

<h1>一、文件操作</h1>
<h2>文件目录函数库</h2>
<h3>文件相关</h3>
<div class="cnblogs_code">
<pre>//获取文件<br />$file_name = "./text.txt";</pre>
<pre><span style="color: #008000;">//</span><span style="color: #008000;">返回文件类型</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">filetype</span>(<span style="color: #800080;">$file_name</span>),'&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">返回文件大小（字节数）</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">filesize</span>(<span style="color: #800080;">$file_name</span>),'&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">返回文件创建时间戳</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">filectime</span>(<span style="color: #800080;">$file_name</span>),'&lt;br&gt;'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">date</span>('Y年m月d日 H:i:s',<span style="color: #008080;">filectime</span>(<span style="color: #800080;">$file_name</span>)),'&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">返回文件修改时间</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">filemtime</span>(<span style="color: #800080;">$file_name</span>),'&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">返回文件最后访问时间</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">fileatime</span>(<span style="color: #800080;">$file_name</span>),'&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">检测是否为文件</span>
<span style="color: #008080;">var_dump</span>(<span style="color: #008080;">is_file</span>(<span style="color: #800080;">$file_name</span><span style="color: #000000;">));
</span><span style="color: #0000ff;">echo</span> '&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">检测文件是否可读、可写、可执行</span>
<span style="color: #008080;">var_dump</span><span style="color: #000000;">(
    </span><span style="color: #008080;">is_readable</span>(<span style="color: #800080;">$file_name</span>),
    <span style="color: #008080;">is_writable</span>(<span style="color: #800080;">$file_name</span>),
    <span style="color: #008080;">is_executable</span>(<span style="color: #800080;">$file_name</span><span style="color: #000000;">)
);</span></pre>
</div>
<p>&nbsp;</p>
<h3>文件路径相关</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$pathinfo</span> = <span style="color: #008080;">pathinfo</span>(<span style="color: #800080;">$file_name</span><span style="color: #000000;">);
</span><span style="color: #008080;">print_r</span>(<span style="color: #800080;">$pathinfo</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">pathinfo</span>(<span style="color: #800080;">$file_name</span>,PATHINFO_DIRNAME),'&lt;br&gt;';<span style="color: #008000;">//</span><span style="color: #008000;">dirname：若是当前目录就为 .</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">pathinfo</span>(<span style="color: #800080;">$file_name</span>,PATHINFO_BASENAME),'&lt;br&gt;';<span style="color: #008000;">//</span><span style="color: #008000;">basename：文件名（包含扩展名）</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">pathinfo</span>(<span style="color: #800080;">$file_name</span>,PATHINFO_FILENAME),'&lt;br&gt;';<span style="color: #008000;">//</span><span style="color: #008000;">filename：文件名</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">pathinfo</span>(<span style="color: #800080;">$file_name</span>,PATHINFO_EXTENSION),'&lt;br&gt;';<span style="color: #008000;">//</span><span style="color: #008000;">extension：扩展名

//输出当前文件完整路径</span>
<span style="color: #800080;">$file_name</span> = <span style="color: #ff00ff;">__FILE__</span>; <span style="color: #008000;">//</span><span style="color: #008000;">获取$file_name的完整路径，包含文件名</span>
<span style="color: #0000ff;">echo</span> <span style="color: #800080;">$file_name</span>,'&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">返回路径中的文件名（含扩展名）</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">basename</span>(<span style="color: #800080;">$file_name</span>),'&lt;br&gt;'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">返回路径中的文件名（过滤掉.php后缀）</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">basename</span>(<span style="color: #800080;">$file_name</span>,'.php'),'&lt;br&gt;'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">返回当前文件的所在路径</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">dirname</span>(<span style="color: #800080;">$file_name</span>),'&lt;br&gt;'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">检测文件或目录是否存在</span>
<span style="color: #008080;">var_dump</span>(<span style="color: #008080;">file_exists</span>(<span style="color: #800080;">$file_name</span>));</pre>
</div>
<p>&nbsp;</p>
<h3>文件操作相关</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">创建文件，若文件存在则进行覆盖</span>
<span style="color: #800080;">$file</span> = '哈哈哈.txt'<span style="color: #000000;">;
</span><span style="color: #0000ff;">if</span>(<span style="color: #008080;">touch</span>(<span style="color: #800080;">$file</span><span style="color: #000000;">))
    </span><span style="color: #0000ff;">echo</span> '文件创建成功'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">删除文件，若文件不存在，还执行删除就会报错</span>
<span style="color: #0000ff;">if</span>(<span style="color: #008080;">file_exists</span>(<span style="color: #800080;">$file</span>) &amp;&amp; <span style="color: #008080;">unlink</span>(<span style="color: #800080;">$file</span><span style="color: #000000;">))
    </span><span style="color: #0000ff;">echo</span> '文件删除成功'<span style="color: #000000;">;
</span><span style="color: #0000ff;">else</span>
    <span style="color: #0000ff;">echo</span> '文件删除失败'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">重命名 || 剪切文件</span>
<span style="color: #0000ff;">if</span>(<span style="color: #008080;">file_exists</span>(<span style="color: #800080;">$file</span>) &amp;&amp; <span style="color: #008080;">rename</span>(<span style="color: #800080;">$file</span>,'我是新名字的.txt'<span style="color: #000000;">))
    </span><span style="color: #0000ff;">echo</span> '重命名成功'<span style="color: #000000;">;
</span><span style="color: #0000ff;">else</span>
    <span style="color: #0000ff;">echo</span> '重命名失败'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">剪切只是在重命名的基础上添加路径</span>
<span style="color: #0000ff;">if</span>(<span style="color: #008080;">file_exists</span>(<span style="color: #800080;">$file</span>) &amp;&amp; <span style="color: #008080;">rename</span>(<span style="color: #800080;">$file</span>,'../我是新名字的.txt'<span style="color: #000000;">))
    </span><span style="color: #0000ff;">echo</span> '剪切成功'<span style="color: #000000;">;
</span><span style="color: #0000ff;">else</span>
    <span style="color: #0000ff;">echo</span> '剪切失败'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">拷贝文件</span>
<span style="color: #0000ff;">if</span>(<span style="color: #008080;">file_exists</span>(<span style="color: #800080;">$file</span>) &amp;&amp; <span style="color: #008080;">copy</span>(<span style="color: #800080;">$file</span>,'../'.<span style="color: #800080;">$file</span><span style="color: #000000;">))
    </span><span style="color: #0000ff;">echo</span> '文件拷贝成功'<span style="color: #000000;">;
</span><span style="color: #0000ff;">else</span>
    <span style="color: #0000ff;">echo</span> '文件拷贝失败'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">也可拷贝远程文件，需要php.ini 开启 allow_url_fopen=On</span>
<span style="color: #0000ff;">if</span>(<span style="color: #008080;">copy</span>('http://baijia-admin.solomore.net/new_baijiabackend/back_end/cover_mp4/upload/1606124640不吼不叫+主动+夫妻.mp4','bbc.mp4'<span style="color: #000000;">))
    </span><span style="color: #0000ff;">echo</span> '文件拷贝成功'<span style="color: #000000;">;
</span><span style="color: #0000ff;">else</span>
    <span style="color: #0000ff;">echo</span> '文件拷贝失败';</pre>
</div>
<p>&nbsp;</p>
<h3>文件内容（打开文件）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = './text.txt'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'r'<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数为文件路径
//第二个参数指定以什么形式打开文件。</span></pre>
</div>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202012/1680452-20201206104830384-2071230946.png" alt="" width="696" height="325" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>文件内容（读取文件）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = './text.txt'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'r'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">读取文件
//$res =  fread($handle,3);
//第一个参数为文件句柄
//第二个参数为读取多少个字节
//注意：若读取到3的位置，指针也会在3的位置，下一次读取的时候是不会从头开始读的</span>

<span style="color: #800080;">$res</span> = <span style="color: #008080;">fread</span>(<span style="color: #800080;">$handle</span>,<span style="color: #008080;">filesize</span>(<span style="color: #800080;">$filename</span>)); <span style="color: #008000;">//</span><span style="color: #008000;">读取全部文件
//echo $res;</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>&nbsp;更好的读取文件操作</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">header("content-type:image/jpeg");</span>
<span style="color: #008080;">header</span>("content-type:video/mp4"); <span style="color: #008000;">//</span><span style="color: #008000;">记得添加输出的文件类型</span>
<span style="color: #800080;">$filename</span> = './bbc.mp4'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'rb+'<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">注意：为了更好的兼容性，在选择打开方式的时候在后面追加一个b

//读取文件</span>
<span style="color: #800080;">$res</span> =  <span style="color: #008080;">fread</span>(<span style="color: #800080;">$handle</span>,<span style="color: #008080;">filesize</span>(<span style="color: #800080;">$filename</span><span style="color: #000000;">));
</span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$res</span><span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">关闭文件</span>
<span style="color: #008080;">fclose</span>(<span style="color: #800080;">$handle</span>);</pre>
</div>
<p>&nbsp;</p>
<p><strong>按字节读 / 按行读</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'ab+'<span style="color: #000000;">);

</span><span style="color: #0000ff;">while</span> (!<span style="color: #008080;">feof</span>(<span style="color: #800080;">$handle</span>)){ <span style="color: #008000;">//</span><span style="color: #008000;">判断当前指针是否已经到文件末尾
    //一个字节一个字节地读
//    echo fgetc($handle)."\n";

    //一行一行地读
//    echo fgets($handle)."\n";

    //一行一行的读，过滤html标签</span>
    <span style="color: #0000ff;">echo</span> <span style="color: #008080;">strip_tags</span>(<span style="color: #008080;">fgets</span>(<span style="color: #800080;">$handle</span>))."\n"<span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>文件内容（文件指针）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">获取当前指针的位置</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">ftell</span>(<span style="color: #800080;">$handle</span><span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数为文件句柄

//设置指针的位置</span>
<span style="color: #008080;">fseek</span>(<span style="color: #800080;">$handle</span>,2<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数为文件句柄
//第二个参数为指针移动到的位置下标</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>文件内容（关闭文件）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = './text.txt'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'r'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">读取文件</span>
<span style="color: #800080;">$res</span> =  <span style="color: #008080;">fread</span>(<span style="color: #800080;">$handle</span>,3<span style="color: #000000;">);
</span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$res</span><span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">关闭文件</span>
<span style="color: #008080;">fclose</span>(<span style="color: #800080;">$handle</span><span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数为文件句柄
//注意：关闭文件后，文件获取到的文件句柄将不可用</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>文件内容（写入文件）</h3>
<p>fwrite的别名是fputs，两者是等价的</p>
<div class="cnblogs_code">
<pre>以读写的形式写入文件r+

<span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'rb+'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">fwrite()执行写入操作</span>
<span style="color: #008080;">fwrite</span>(<span style="color: #800080;">$handle</span>,'我要写入文字',6<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数为文件句柄
//第二个参数为写入的内容
//第三个可选参数，表示写入的长度，默认全部写入
//注意：写入的内容会覆盖原来的内容，写入到哪个地方指针就会在哪里停留</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">以写入的形式打开文件w。若文件存在则截断为0后写入；若文件不存在则会先创建

</span><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'w'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">fwrite()执行写入操作</span>
<span style="color: #008080;">fwrite</span>(<span style="color: #800080;">$handle</span>,'我要'.PHO_EOL.'写入文字'); <span style="color: #008000;">//</span><span style="color: #008000;">PHP_EOL已弃用
//第一个参数为文件句柄
//第二个参数为写入的内容
//第三个可选参数，表示写入的长度，默认全部写入
//注意：写入的内容会覆盖原来的内容，写入到哪个地方指针就会在哪里停留</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>以写入的形式打开文件a  a+<span style="color: #000000;">是读写的形式
若文件存在，则指针跳到文件末尾后写入；若文件不存在则会先创建

</span><span style="color: #008000;">//</span><span style="color: #008000;">打开文件b</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'ab+'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">fwrite()执行写入操作</span>
<span style="color: #008080;">fwrite</span>(<span style="color: #800080;">$handle</span>,'我要写入文字'."\n"<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数为文件句柄
//第二个参数为写入的内容
//第三个可选参数，表示写入的长度，默认全部写入
//注意：写入的内容会覆盖原来的内容，写入到哪个地方指针就会在哪里停留</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>想要输出追加后的所有内容</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">文件写入后想读取文件的所有内容，需要先重置指针</span>
<span style="color: #008080;">rewind</span>(<span style="color: #800080;">$handle</span><span style="color: #000000;">);

</span><span style="color: #800080;">$res</span> = <span style="color: #008080;">fread</span>(<span style="color: #800080;">$handle</span>,<span style="color: #008080;">filesize</span>(<span style="color: #800080;">$filename</span><span style="color: #000000;">));
</span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$res</span>;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>想要截断文件，源文件会被修改</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">打开文件b</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'ab+'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">将文件截断成自己需要的部分</span>
<span style="color: #008080;">ftruncate</span>(<span style="color: #800080;">$handle</span>,9);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>CSV文件操作</h3>
<p>将csv里面的数据全部转为数组</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'rb+'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">读取里面的全部内容，并转为数组</span>
<span style="color: #0000ff;">while</span> (<span style="color: #800080;">$row</span> = <span style="color: #008080;">fgetcsv</span>(<span style="color: #800080;">$handle</span>)){ <span style="color: #008000;">//</span><span style="color: #008000;">只要$row不等于空就继续循环</span>
    <span style="color: #800080;">$arr</span>[] = <span style="color: #800080;">$row</span><span style="color: #000000;">;
}
</span><span style="color: #008080;">print_r</span>(<span style="color: #800080;">$arr</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>若csv文件里面的分隔符不是 , 的话</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'rb+'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">读取里面的全部内容，并转为数组</span>
<span style="color: #0000ff;">while</span> (<span style="color: #800080;">$row</span> = <span style="color: #008080;">fgetcsv</span>(<span style="color: #800080;">$handle</span>,0,'-'<span style="color: #000000;">)){ 
    </span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数文件句柄，
    //第二个参数表示读多少行 0表示全读，默认为0
    //第三个参数说明csv里面的分隔符</span>
    <span style="color: #800080;">$arr</span>[] = <span style="color: #800080;">$row</span><span style="color: #000000;">;
}
</span><span style="color: #008080;">print_r</span>(<span style="color: #800080;">$arr</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>将数组写入csv文件</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">打开文件</span>
<span style="color: #800080;">$handle</span> = <span style="color: #008080;">fopen</span>(<span style="color: #800080;">$filename</span>,'wb+'<span style="color: #000000;">);

</span><span style="color: #800080;">$arr</span> =<span style="color: #000000;">[
    [</span>1,'男',23,'北京','sldkfjl@163.com'],<span style="color: #000000;">
    [</span>1,'男',23,'北京','sldkfjl@163.com'],<span style="color: #000000;">
    [</span>1,'男',23,'北京','sldkfjl@163.com'],<span style="color: #000000;">
    [</span>1,'男',23,'北京','sldkfjl@163.com'],<span style="color: #000000;">
    [</span>1,'男',23,'北京','sldkfjl@163.com'<span style="color: #000000;">]
];

</span><span style="color: #008000;">//</span><span style="color: #008000;">写入csv文件</span>
<span style="color: #0000ff;">foreach</span> (<span style="color: #800080;">$arr</span> <span style="color: #0000ff;">as</span> <span style="color: #800080;">$val</span><span style="color: #000000;">){
    fputcsv(</span><span style="color: #800080;">$handle</span>,<span style="color: #800080;">$val</span>,'-'<span style="color: #000000;">);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数为文件句柄
    //第二个参数为一个一维数组
    //第三个可选参数，表示写入csv文件的分隔符，默认逗号</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>常用读取文件操作</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">读取文件
//$filename = './aa.csv';

//读取视频
//header("content-type:video/mp4");
//$filename = './bbc.mp4';

//读取html</span>
<span style="color: #008080;">header</span>("content-type:text/html;charset=utf-8"<span style="color: #000000;">);
</span><span style="color: #800080;">$filename</span> = 'http://www.baidu.com'<span style="color: #000000;">;

</span><span style="color: #800080;">$res</span> = <span style="color: #008080;">file_get_contents</span>(<span style="color: #800080;">$filename</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$res</span>;</pre>
</div>
<p>&nbsp;</p>
<h3>常用写入文件操作（覆盖原来的）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = 'text.txt'<span style="color: #000000;">;
</span><span style="color: #008080;">file_put_contents</span>(<span style="color: #800080;">$filename</span>,'haha,I\'m a text');</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>常用写入文件操作（文件最后追加内容）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = 'text.txt'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">获取原来内容</span>
<span style="color: #800080;">$str</span> = <span style="color: #008080;">file_get_contents</span>(<span style="color: #800080;">$filename</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">定义新内容</span>
<span style="color: #800080;">$new_date</span> = <span style="color: #800080;">$str</span>.'haha,I\'m a new text'."\n"<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">进行数据写入</span>
<span style="color: #008080;">file_put_contents</span>(<span style="color: #800080;">$filename</span>,<span style="color: #800080;">$new_date</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">显示全部内容</span>
<span style="color: #800080;">$res</span> = <span style="color: #008080;">file_get_contents</span>(<span style="color: #800080;">$filename</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$res</span><span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">注意：file_put_content函数，若文件不存在会进行创建</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>常用写入文件操作（将数组写入文件）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = 'text.txt'<span style="color: #000000;">;
</span><span style="color: #800080;">$arr</span> =<span style="color: #000000;"> [
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
];

</span><span style="color: #008000;">//</span><span style="color: #008000;">先将数组序列化</span>
<span style="color: #800080;">$date</span> = <span style="color: #008080;">serialize</span>(<span style="color: #800080;">$arr</span><span style="color: #000000;">);
</span><span style="color: #008080;">file_put_contents</span>(<span style="color: #800080;">$filename</span>,<span style="color: #800080;">$date</span>);</pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;</h3>
<h3>常用写入文件操作（将文件里的序列化数据，转为数组）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = 'text.txt'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">获取文件里面的序列化数据</span>
<span style="color: #800080;">$date</span> = <span style="color: #008080;">file_get_contents</span>(<span style="color: #800080;">$filename</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">将序列化数据转为数组</span>
<span style="color: #800080;">$arr</span> = <span style="color: #008080;">unserialize</span>(<span style="color: #800080;">$date</span><span style="color: #000000;">);
</span><span style="color: #008080;">print_r</span>(<span style="color: #800080;">$arr</span>);</pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;</h3>
<h3>常用写入文件操作（array转json，json转array）</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$filename</span> = 'text.txt'<span style="color: #000000;">;
</span><span style="color: #800080;">$arr</span> =<span style="color: #000000;"> [
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
    [</span>1,'小明',23,'男','北京'],<span style="color: #000000;">
];
</span><span style="color: #008000;">//</span><span style="color: #008000;">将数组转为json字符串，并存入文件</span>
<span style="color: #800080;">$date</span> = json_encode(<span style="color: #800080;">$arr</span><span style="color: #000000;">);
</span><span style="color: #008080;">file_put_contents</span>(<span style="color: #800080;">$filename</span>,<span style="color: #800080;">$date</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">///////////////////////////////////////////</span>

<span style="color: #800080;">$filename</span> = 'text.txt'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">读取文件里的json数据，并转为数组</span>
<span style="color: #800080;">$date</span> = <span style="color: #008080;">file_get_contents</span>(<span style="color: #800080;">$filename</span><span style="color: #000000;">);
</span><span style="color: #800080;">$arr</span> = json_decode(<span style="color: #800080;">$date</span><span style="color: #000000;">);
</span><span style="color: #008080;">print_r</span>(<span style="color: #800080;">$arr</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h1>二、Mysql基础</h1>
<p>略</p>
<p>&nbsp;</p>
<h1>三、PHP操作MySQL</h1>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202012/1680452-20201206192137737-2089970047.png" alt="" width="758" height="311" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">连接数据库</span>
<span style="color: #800080;">$conn</span> = <span style="color: #008080;">mysqli_connect</span>('host','user','password','new_database','3306'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">判断是否连接成功</span>
<span style="color: #0000ff;">if</span>(<span style="color: #008080;">mysqli_connect_error</span>() != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    </span><span style="color: #0000ff;">die</span>('连接失败：'.<span style="color: #008080;">mysqli_connect_error</span><span style="color: #000000;">());
</span><span style="color: #0000ff;">else</span>
    <span style="color: #0000ff;">echo</span> '连接成功'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">选择数据库</span>
<span style="color: #008080;">mysqli_select_db</span>(<span style="color: #800080;">$conn</span>,'other_database'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">设置字符集</span>
mysqli_set_charset(<span style="color: #800080;">$conn</span>,'utf8'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">书写sql语句</span>
<span style="color: #800080;">$sql</span> = 'SELECT * FROM table'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">执行sql</span>
<span style="color: #800080;">$result</span> = <span style="color: #008080;">mysqli_query</span>(<span style="color: #800080;">$conn</span>,<span style="color: #800080;">$sql</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">解析结果集
//$array = mysqli_fetch_array($result);//解析为索引数组</span>
<span style="color: #800080;">$array</span> = <span style="color: #008080;">mysqli_fetch_assoc</span>(<span style="color: #800080;">$result</span>);<span style="color: #008000;">//</span><span style="color: #008000;">解析为关联数组

//关闭连接</span>
<span style="color: #008080;">mysqli_close</span>(<span style="color: #800080;">$conn</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>解析结果集的方法</h2>
<h3>逐条解析</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">索引数组和关联数组并存</span>
<span style="color: #008080;">mysqli_fetch_array</span>(<span style="color: #800080;">$result</span>);<span style="color: #008000;">//</span><span style="color: #008000;">默认就是MYSQLI_BOTH</span>
<span style="color: #008080;">mysqli_fetch_array</span>(<span style="color: #800080;">$result</span>,<span style="color: #000000;">MYSQLI_BOTH);

</span><span style="color: #008000;">//</span><span style="color: #008000;">只有索引数组</span>
<span style="color: #008080;">mysqli_fetch_row</span>(<span style="color: #800080;">$result</span><span style="color: #000000;">);
</span><span style="color: #008080;">mysqli_fetch_array</span>(<span style="color: #800080;">$result</span>,<span style="color: #000000;">MYSQLI_NUM);

</span><span style="color: #008000;">//</span><span style="color: #008000;">只有关联数组</span>
<span style="color: #008080;">mysqli_fetch_assoc</span>(<span style="color: #800080;">$result</span><span style="color: #000000;">);
</span><span style="color: #008080;">mysqli_fetch_array</span>(<span style="color: #800080;">$result</span>,<span style="color: #000000;">MYSQLI_ASSOC);

</span><span style="color: #008000;">//</span><span style="color: #008000;">解析成对象形式</span>
<span style="color: #008080;">mysqli_fetch_object</span>(<span style="color: #800080;">$result</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>全部解析</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">索引数组和关联数组并存</span>
mysqli_fetch_all(<span style="color: #800080;">$result</span>,<span style="color: #000000;">MYSQLI_BOTH);

</span><span style="color: #008000;">//</span><span style="color: #008000;">只有索引数组</span>
mysqli_fetch_all(<span style="color: #800080;">$result</span><span style="color: #000000;">);
mysqli_fetch_all(</span><span style="color: #800080;">$result</span>,MYSQLI_NUM);<span style="color: #008000;">//</span><span style="color: #008000;">默认

//只有关联数组</span>
mysqli_fetch_all(<span style="color: #800080;">$result</span>,MYSQLI_ASSOC);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>功能性函数</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">获取到的结果的行</span>
<span style="color: #800080;">$n</span> = <span style="color: #008080;">mysqli_num_rows</span>(<span style="color: #800080;">$result</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取到结果的列数</span>
<span style="color: #800080;">$colum</span> = <span style="color: #008080;">mysqli_num_fields</span>(<span style="color: #800080;">$result</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">还可以查询刚才插入的数据id</span>
<span style="color: #800080;">$id</span> = <span style="color: #008080;">mysqli_insert_id</span>(<span style="color: #800080;">$conn</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">执行完sql语句可以查询到影响的行数</span>
<span style="color: #800080;">$num</span> = <span style="color: #008080;">mysqli_affected_rows</span>(<span style="color: #800080;">$conn</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">逐条解析时的，循环输出</span>
<span style="color: #0000ff;">while</span>(<span style="color: #800080;">$row</span> = <span style="color: #008080;">mysqli_fetch_assoc</span>(<span style="color: #800080;">$result</span><span style="color: #000000;">)){
    </span><span style="color: #008080;">print_r</span>(<span style="color: #800080;">$row</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h1>四、会话控制</h1>
<h2>会话控制的方式</h2>
<p>1、COOKIE</p>
<p>2、SESSION</p>
<p>3、其他：</p>
<p>Json Web Tocken：json格式令牌，用于系统间交互</p>
<p>Authorized Tocken：用于系统对用授权</p>
<p>Access Tocken + Secret Tocken：用于对用户进行资源的访问限制</p>
<p>&nbsp;</p>
<h2>COOKIE</h2>
<p>作用：cookie可以标记用户、标记客户端、存储简单值</p>
<p>&nbsp;</p>
<p>工作原理：在http响应时，给客户端设置cookie；在cookie有效期内，每次请求都会携带cookie的值</p>
<p>&nbsp;</p>
<h3><strong>cookie的生命周期：</strong></h3>
<p><strong>在http请求中携带cookie</strong></p>
<p>1、只可访问域名相同，路径匹配并在有效期内的cookie</p>
<p>2、通过cookie指令发送具有访问权限的cookie值</p>
<p>3、多个cookie的值用分号; 隔开</p>
<p><strong>cookie失效</strong></p>
<p>1、cookie过期</p>
<p>2、用户手动删除cookie</p>
<p>3、服务器清楚cookie有效性</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>SESSION</h2>
<p>作用：cookie可以标记用户、标记客户端、存储数据 (其中可以大数据)</p>
<p>&nbsp;</p>
<p>工作原理：</p>
<p>1、在http响应中设置cookie，并在临时文件中保存session值</p>
<p>2、通过客户端请求中的cookie定位到相应的session文件</p>
<p>3、读取并处理session的内容</p>
<p>&nbsp;</p>
<h3><strong>SESSION的生命周期：</strong></h3>
<p><strong>启用并设置cookie：</strong></p>
<p>1、在http响应中设置客户端的唯一cookie</p>
<p>2、将相应的session内容写入临时文件</p>
<p><strong>读取并处理session：</strong></p>
<p>1、客户端在http请求中携带cookie的值</p>
<p>2、服务器通过cookie值定位到session文件</p>
<p>3、读取并处理session内容</p>
<p><strong>SESSION失效 / 清除：</strong></p>
<p>1、cookie过期（关闭浏览器）</p>
<p>2、用户手动删除cookie</p>
<p>3、服务端删除session文件 或 清空session内容</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>SESSION的使用</h3>
<p>session开启前设置（若需要的话）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">获取 / 设置SESSION NAME 的值</span>
<span style="color: #008080;">session_name</span>('se_name'); <span style="color: #008000;">//</span><span style="color: #008000;">设置了session_name的值</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">session_name</span>();<span style="color: #008000;">//</span><span style="color: #008000;">获取了session_name的值

//获取 / 设置SESSION ID 的值</span>
<span style="color: #008080;">session_id</span>('2323'<span style="color: #000000;">);
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">session_id</span><span style="color: #000000;">();

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取 / 设置SESSION文件的保存路径</span>
<span style="color: #008080;">session_save_path</span>('/'<span style="color: #000000;">);
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">session_save_path</span><span style="color: #000000;">();

</span><span style="color: #008000;">//</span><span style="color: #008000;">设置SESSION中的COOKIE参数</span>
<span style="color: #008080;">session_set_cookie_params</span><span style="color: #000000;">();
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数：cookie生存时间 int
//第二个参数：cookie的有效路径 string
//第三个参数：有效域名 string
//第四个参数：安全限制，默认false bool
//第五个参数：访问限制，默认false bool

//注意：以上设置需要在session开启之前设置</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>开启session并使用</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">开启session</span>
<span style="color: #008080;">session_start</span><span style="color: #000000;">();

</span><span style="color: #008000;">//</span><span style="color: #008000;">设置session的值</span>
<span style="color: #800080;">$_SESSION</span>['user'] = <span style="color: #0000ff;">array</span><span style="color: #000000;">(
    </span>'username' =&gt; '人',
    'age' =&gt; 23<span style="color: #000000;">
);

</span><span style="color: #008000;">//</span><span style="color: #008000;">读取session的内容</span>
<span style="color: #008080;">var_dump</span>(<span style="color: #800080;">$_SESSION</span>['user'<span style="color: #000000;">]);

</span><span style="color: #008000;">//</span><span style="color: #008000;">清空session数据,session文件还会存在</span>
<span style="color: #008080;">session_unset</span><span style="color: #000000;">();
</span><span style="color: #008000;">//</span><span style="color: #008000;">删除session文件</span>
<span style="color: #008080;">session_destroy</span>();</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>利用COOKIE实现记住用户登录状态</h2>
<p>登录成功后设置cookie保存到本地</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">setcookie</span>('username',<span style="color: #800080;">$username</span>,<span style="color: #008080;">time</span>() + 7 * 24 * 3600);<span style="color: #008000;">//</span><span style="color: #008000;">设置用户名、和cookie有效时间7天</span></pre>
</div>
<p>&nbsp;</p>
<p>网页中检查cookie是否存在 并 合法性。若是检查无误后，设置Session值</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">session_start</span><span style="color: #000000;">();

</span><span style="color: #0000ff;">if</span>(<span style="color: #0000ff;">isset</span>(<span style="color: #800080;">$_SESSION</span>['username']) &amp;&amp; <span style="color: #800080;">$_SESSION</span>['username']=='people'<span style="color: #000000;">)
    </span><span style="color: #0000ff;">echo</span> '登录成功'<span style="color: #000000;">;
</span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span>(<span style="color: #0000ff;">isset</span>(<span style="color: #800080;">$_COOKIE</span>['username']) &amp;&amp; <span style="color: #800080;">$_COOKIE</span>['username']=='people'<span style="color: #000000;">){
    </span><span style="color: #800080;">$_SESSION</span>['username'] = 'people'<span style="color: #000000;">;
    </span><span style="color: #0000ff;">echo</span> '登录成功'<span style="color: #000000;">;
}
</span><span style="color: #0000ff;">else</span>
    <span style="color: #008080;">header</span>("Location:login.php");</pre>
</div>
<p>&nbsp;</p>
<p>注销登录时，不仅要清楚session，还要清除cookie</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">session_unset</span><span style="color: #000000;">();
</span><span style="color: #008080;">setcookie</span>('username','',<span style="color: #008080;">time</span>()-33);</pre>
</div>
<p>&nbsp;</p>
