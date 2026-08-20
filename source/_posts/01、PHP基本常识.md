---
title: "01、PHP基本常识"
date: "2020-07-24 09:22:00"
updated: "2020-09-06 19:54:00"
tags:
categories:
description: >-
  1、变量和数据类型 变量$ + 符合命名规范的字符 php是一种弱类型语言，即不需要生命变量类型就能够使用。 变量输出：echo + 字符串/变量，var_dump(变量) 输出变量类型及数据 注释：单行注释// 或 #，多行注释 /**/ 指定编码方式： //告诉浏览器以什么编码方式解析什么类型的
---

<h2><strong>1、变量和数据类型</strong></h2>
<p><strong>变量</strong>$ + 符合命名规范的字符</p>
<p>php是一种弱类型语言，即不需要生命变量类型就能够使用。</p>
<p>&nbsp;</p>
<p><strong>变量输出</strong>：echo + 字符串/变量，var_dump(变量) 输出变量类型及数据</p>
<p><strong>注释</strong>：单行注释// 或 #，多行注释 /**/</p>
<p>&nbsp;</p>
<p><strong>指定编码方式</strong>：</p>
<p>//告诉浏览器以什么编码方式解析什么类型的文档</p>
<div class="cnblogs_code">
<pre>header('content-type:text/html;charset=utf-8');</pre>
</div>
<p>&nbsp;</p>
<p><strong>错误抑制符</strong>：@&nbsp; &nbsp; //在某个语句前添加@可以忽略该语句的错误信息</p>
<h3><strong>变量类型</strong>：</h3>
<p>浮点型$a = 2e3 / $a = 2E3 就是 2x10的3次方&nbsp;</p>
<p>字符串型 ' '里面内容不解析变量，" "里面内容解析变量，" "可以尝试字符串加变量一起输出。</p>
<div class="cnblogs_code">
<pre>$name = <span style="color: #800000;">'</span><span style="color: #800000;">丘</span><span style="color: #800000;">'</span><span style="color: #000000;">;
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">我是$name 的啊</span><span style="color: #800000;">"</span>;<span style="color: #008000;">//</span><span style="color: #008000;">$name 后要用空格隔开，否则就会被认为后面一串都是变量名。
</span><span style="color: #008000;">//</span><span style="color: #008000;">若不想要空格还可以这样，{}里面不能有空格，否则就会被当做普通字符</span>
echo <span style="color: #800000;">"</span><span style="color: #800000;">我是{$name}的啊</span><span style="color: #800000;">"</span><span style="color: #000000;">;
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">我是${name} 的啊</span><span style="color: #800000;">"</span>;</pre>
</div>
<p>转义符：\n回车，\t水平制表符，\r回车，\\是\，\$是$，\'是'，\*是*</p>
<p>略......</p>
<p>&nbsp;</p>
<h3>类型转换</h3>
<h4><strong>临时转换（不改变变量本身）</strong></h4>
<p>第一种：(变量类型)变量名称。如：$bb = (int)$a;&nbsp; //将$a转换为整型</p>
<div class="cnblogs_code">
<pre>(<span style="color: #0000ff;">int</span>)(integer)、(<span style="color: #0000ff;">float</span>)(<span style="color: #0000ff;">double</span>)(real)、(<span style="color: #0000ff;">string</span>)、(<span style="color: #0000ff;">bool</span><span style="color: #000000;">)(boolean)

(unset)   </span><span style="color: #008000;">//</span><span style="color: #008000;">将某变量临时转换为 null</span>
(array)   <span style="color: #008000;">//</span><span style="color: #008000;">临时将变量转换为数组</span>
(<span style="color: #0000ff;">object</span>)   <span style="color: #008000;">//</span><span style="color: #008000;">临时将变量转换为对象</span></pre>
</div>
<p>第二种：通过系统函数。即 变量类型val(变量名称)，如 $a = intval($b);&nbsp; //将$b转换为整型</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">intval
floatval、doubleval
stringval
boolval</span></pre>
</div>
<p>&nbsp;</p>
<h4><strong>永久转换（改变变量本身）</strong></h4>
<p>gettype（获取变量类型，慎用）</p>
<div class="cnblogs_code">
<pre>echo gettype($a); <span style="color: #008000;">//</span><span style="color: #008000;">输出$a的变量类型</span></pre>
</div>
<p>settype($a,'int') （设置变量类型）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">例子</span>
$a = <span style="color: #800080;">1</span><span style="color: #000000;">;
settype($a,</span><span style="color: #800000;">'</span><span style="color: #800000;">bool</span><span style="color: #800000;">'</span><span style="color: #000000;">);
var_dump($a);

</span><span style="color: #008000;">//</span><span style="color: #008000;">类型参数</span>
boolean/<span style="color: #0000ff;">bool</span><span style="color: #000000;">
integer</span>/<span style="color: #0000ff;">int</span>
<span style="color: #0000ff;">float</span>
<span style="color: #0000ff;">string</span><span style="color: #000000;">
array
</span><span style="color: #0000ff;">object</span>
<span style="color: #0000ff;">null</span></pre>
</div>
<p>&nbsp;</p>
<h4>&nbsp;通过变量函数库，检测变量类型</h4>
<p>is_类型(变量);&nbsp; &nbsp;//检测变量是不是该类型，返回bool&nbsp;</p>
<p>如检测 $a是不是整型，is_int($a);&nbsp; //返回bool</p>
<p>&nbsp;</p>
<p>如检测 $c是不是资源</p>
<div class="cnblogs_code">
<pre>$c = fopen(<span style="color: #800000;">'</span><span style="color: #800000;">./cc.html</span><span style="color: #800000;">'</span> , <span style="color: #800000;">'</span><span style="color: #800000;">r</span><span style="color: #800000;">'</span><span style="color: #000000;">);
echo is_resource($c);  </span><span style="color: #008000;">//</span><span style="color: #008000;">输出true</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">类型</span>
<span style="color: #000000;">
整型：is_int() , is_integer() , is_long()

浮点型：is_float() , is_double() , is_real()

字符串：is_string()

布尔型：is_bool()

标量类型：is_scalar()

空null：is_null()

数组：is_array()

对象：is_object()

资源：is_resource

是否为数值型</span>/字符串形式的数值：is_numeric()</pre>
</div>
<p>&nbsp;</p>
<h3>heredoc 和 nowdoc</h3>
<p>heredoc相当于 " " ，使用语法</p>
<div class="cnblogs_code">
<pre>$str = &lt;&lt;&lt;<span style="color: #000000;">haha
这里是代码段
haha;
echo $str;

</span><span style="color: #008000;">//</span><span style="color: #008000;">也可以</span>
$str = &lt;&lt;&lt;<span style="color: #800000;">"</span><span style="color: #800000;">haha</span><span style="color: #800000;">"</span><span style="color: #000000;">
这里是代码段
haha;
echo $str;</span></pre>
</div>
<p>&nbsp;</p>
<p>nowdoc相当于 ' ' ，使用语法</p>
<div class="cnblogs_code">
<pre>$str = &lt;&lt;&lt;<span style="color: #800000;">'</span><span style="color: #800000;">now</span><span style="color: #800000;">'</span><span style="color: #000000;">
这里的变量不会被解析到
now;</span></pre>
</div>
<p>&nbsp;</p>
<h2>2、PHP常量</h2>
<h3>php系统常量</h3>
<div class="cnblogs_code">
<pre>echo PHP_VERSION; <span style="color: #008000;">//</span><span style="color: #008000;">输出php的版本</span>
<span style="color: #000000;">
echo PHP_OS; </span><span style="color: #008000;">//</span><span style="color: #008000;">输出php的系统</span>
<span style="color: #000000;">
echo PHP_INT_MAX;</span><span style="color: #008000;">//</span><span style="color: #008000;">整型的最大值</span>
<span style="color: #000000;">
略。。。</span></pre>
</div>
<p>&nbsp;</p>
<h3>php自定义常量</h3>
<p>define函数</p>
<div class="cnblogs_code">
<pre>define(<span style="color: #800000;">'</span><span style="color: #800000;">NAME</span><span style="color: #800000;">'</span><span style="color: #000000;">,VALUE);
echo NAME;

</span><span style="color: #008000;">//</span><span style="color: #008000;">常量名称最好大写,常量名称不能加$，常量是全局的作用域
</span><span style="color: #008000;">//</span><span style="color: #008000;">常量已经定义，在脚本执行期间是不可改变的</span></pre>
</div>
<p>&nbsp;</p>
<p>const关键字</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">const</span> NAME =<span style="color: #000000;"> VALUE;
echo NAME;</span></pre>
</div>
<p>&nbsp;</p>
<p>魔术常量</p>
<div class="cnblogs_code">
<pre>__LINE__  <span style="color: #008000;">//</span><span style="color: #008000;">得到当前的行号</span>
<span style="color: #000000;">
__FILE__  </span><span style="color: #008000;">//</span><span style="color: #008000;">得到当前文件完整的绝对路径和文件名</span>
<span style="color: #000000;">
__DIR__  </span><span style="color: #008000;">//</span><span style="color: #008000;">得到当前文件完整的绝对路径</span>
<span style="color: #000000;">
__FUNCTION__  </span><span style="color: #008000;">//</span><span style="color: #008000;">得到当前函数的名称</span>
<span style="color: #000000;">
__CLASS__  </span><span style="color: #008000;">//</span><span style="color: #008000;">得到当前类的类名</span>
<span style="color: #000000;">
__METHOD__  </span><span style="color: #008000;">//</span><span style="color: #008000;">得到当前类的方法名称</span>
<span style="color: #000000;">
__TRAIT__  </span><span style="color: #008000;">//</span><span style="color: #008000;">得到当前TRAIT名称</span>
<span style="color: #000000;">
__NAMESPACE__  </span><span style="color: #008000;">//</span><span style="color: #008000;">得到当前命名空间的名称</span></pre>
</div>
<p>&nbsp;</p>
<p>使用常量</p>
<p>1、直接写常量名称</p>
<p>2、通过 constant('NAME')，如echo constant('NAME')；</p>
<p>&nbsp;</p>
<p>检测常量是否存在</p>
<p>defined('NAME');&nbsp; //返回bool</p>
<p>&nbsp;</p>
<p>得到所有已经定义的产量，及系统常量（数组）</p>
<div class="cnblogs_code">
<pre>print_r(get_defined_contants());</pre>
</div>
<p>&nbsp;</p>
<p>输出</p>
<div class="cnblogs_code">
<pre>echo <span style="color: #008000;">//</span><span style="color: #008000;">输出一个或多个字符串</span>
<span style="color: #000000;">
print_r()  </span><span style="color: #008000;">//</span><span style="color: #008000;">打印数组信息</span>
<span style="color: #000000;">
var_dump()  </span><span style="color: #008000;">//</span><span style="color: #008000;">打印变量的详细信息，一个或多个都行</span></pre>
</div>
<p>&nbsp;</p>
<h3>PHP预定义变量</h3>
<p>$GLOBALS&nbsp; //超全局变量，包含以下所有的预定义变量</p>
<p>$_SERVERS&nbsp; //服务器和执行环境信息变量</p>
<p>$_ENV&nbsp; //环境变量</p>
<p>$_COOKIE&nbsp; //Http cookies</p>
<p>$_SESSION&nbsp; //http session</p>
<p>$_FILES&nbsp; //文件上传信息变量</p>
<p>$_GET&nbsp; &nbsp; //接收以get方式方式发送的数据</p>
<p>$_POST //接收以post方式发送的数据</p>
<p>$_REQUEST&nbsp; //$_GET + $_POST + $_COOKIE</p>
<div class="cnblogs_code">
<pre>print_r($_GET);  <span style="color: #008000;">//</span><span style="color: #008000;">接收以get方式接收的所有数据，以数组的方式存起来<br /><br />echo $_REQUEST['name'];  //接收get/post发送的数据</span></pre>
</div>
<p>&nbsp;</p>
<h2>3、运算符</h2>
<p>算术运算符</p>
<p>递增递减运算符</p>
<p>字符连接符</p>
<p>赋值运算符</p>
<p>比较运算符</p>
<p>逻辑运算符</p>
<p>错误抑制符</p>
<p>略。。。</p>
<p>&nbsp;</p>
<h2>4、流程控制</h2>
<p>if</p>
<p>switch...case</p>
<p>for</p>
<p>while,do while,goto</p>
<p>略。。。</p>
