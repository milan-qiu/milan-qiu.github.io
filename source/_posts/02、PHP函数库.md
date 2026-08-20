---
title: "02、PHP函数库"
date: "2020-09-05 19:07:00"
tags:
categories:
description: >-
  1、自定义函数 局部变量：函数内部定义的变量，只能内部使用 全局变量：从函数定义后的地方，一直到代码结尾都可以使用 超全局变量：函数内/外定义的函数，在哪里都可以被访问 //超全局变量 $GLOBALS $_SERVER $_GET/$_POST $_FILES $_COOKIE $_REQUEST
---

<h2>1、自定义函数</h2>
<p>局部变量：函数内部定义的变量，只能内部使用</p>
<p>全局变量：从函数定义后的地方，一直到代码结尾都可以使用</p>
<p>超全局变量：函数内/外定义的函数，在哪里都可以被访问</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">超全局变量</span>
<span style="color: #000000;">$GLOBALS
$_SERVER
$_GET</span>/<span style="color: #000000;">$_POST
$_FILES
$_COOKIE
$_REQUEST
$_SESSION</span></pre>
</div>
<p>&nbsp;</p>
<p>跟标识符命名规则相同，必须驼峰标记法，所有函数都是全局作用域，不支持重载、不支持取消定义、不支持重定义已声明的函数</p>
<p><strong>定义及使用：</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">function add($a,$b){
  echo $a</span>+<span style="color: #000000;">$b;
}
add(</span><span style="color: #800080;">1</span>,<span style="color: #800080;">2</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">或者</span>
<span style="color: #000000;">function add($a,$b){
  </span><span style="color: #0000ff;">return</span> $a+<span style="color: #000000;">$b;
}
$c </span>= add(<span style="color: #800080;">1</span>,<span style="color: #800080;">2</span>);</pre>
</div>
<p>&nbsp;</p>
<p><strong>函数内对全局变量进行操作：</strong>$GLOBALS(超全局变量)&nbsp; 或者 global 关键字实现</p>
<div class="cnblogs_code">
<pre>$n = <span style="color: #800080;">1</span><span style="color: #000000;">;
function add(){
  $GLOBALS[</span><span style="color: #800000;">'</span><span style="color: #800000;">n</span><span style="color: #800000;">'</span>]++<span style="color: #000000;">;
  echo $n;  </span><span style="color: #008000;">//</span><span style="color: #008000;">2</span>
<span style="color: #000000;">}
add();</span></pre>
</div>
<p>echo strrpos('name','a');&nbsp; //从最后开始找，返回a在字符串里面的下标</p>
<p>echo substr('name',1);&nbsp; //截取字符串，从第1位开始截，返回截取后的值</p>
<p>echo strtolower('HELLO');&nbsp; //将大写转换为小写</p>
<p>&nbsp;</p>
<h3>引用传值</h3>
<p>引用传值必须在参数的前面加上 &amp; 符号</p>
<p>引用传值的参数只能是变量</p>
<p>引用传值会改变函数外的值</p>
<p>引用指向原始变量</p>
<div class="cnblogs_code">
<pre>$a = <span style="color: #800000;">'</span><span style="color: #800000;">hahaha</span><span style="color: #800000;">'</span><span style="color: #000000;">;

$b </span>= &amp;$a; <span style="color: #008000;">//</span><span style="color: #008000;">将$a的原始值指向$b，$b改变$a也改变</span>
<span style="color: #000000;">
$b </span>= <span style="color: #800000;">'</span><span style="color: #800000;">xixixi</span><span style="color: #800000;">'</span>; <span style="color: #008000;">//</span><span style="color: #008000;">这样$a的原始值就会改变</span>
<span style="color: #000000;">
echo $a;  </span><span style="color: #008000;">//</span><span style="color: #008000;">这里会输出 'xixixi'</span></pre>
</div>
<p>&nbsp;</p>
<p>实例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">function ha($a){
  $a</span>++<span style="color: #000000;">;
  echo $a; </span><span style="color: #008000;">//</span><span style="color: #008000;">这里是34</span>
<span style="color: #000000;">}
$a </span>= <span style="color: #800080;">33</span><span style="color: #000000;">;
ha($a); </span><span style="color: #008000;">//</span><span style="color: #008000;">这里是34（局部的）</span><span style="color: #000000;">
echo $a; </span><span style="color: #008000;">//</span><span style="color: #008000;">这里仍然是33（全局的）</span>

<span style="color: #808080;">//////</span><span style="color: #008000;">/ 函数内部不能改变函数外部的值，但利用引用传值可以，如： </span><span style="color: #808080;">//////</span><span style="color: #008000;">/</span>
<span style="color: #000000;">
function ha(</span>&amp;<span style="color: #000000;">$a){
  $a</span>++<span style="color: #000000;">;
  echo $a; </span><span style="color: #008000;">//</span><span style="color: #008000;">这里是34</span>
<span style="color: #000000;">}
$a </span>= <span style="color: #800080;">33</span><span style="color: #000000;">;
ha($a); </span><span style="color: #008000;">//</span><span style="color: #008000;">这里是34（局部的）</span>
echo $a; <span style="color: #008000;">//</span><span style="color: #008000;">这里是34（全局的）</span></pre>
</div>
<p>&nbsp;</p>
<h3>可变参数</h3>
<p>php5.5前</p>
<p>func_get_args()&nbsp; //获取所有参数，并组合成数组，</p>
<p>func_get_arg()&nbsp; //获取传递给函数的某一项</p>
<p>func_num_args();&nbsp; //获取参数的数量</p>
<p>array_sum();&nbsp; //对数组所有值求和</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">function avg(){
  $arr </span>=<span style="color: #000000;"> func_get_args();
  print_r($arr); </span><span style="color: #008000;">//</span><span style="color: #008000;">这里会获取到所有传递过来的参数的数组
  
  </span><span style="color: #008000;">//</span><span style="color: #008000;">对接收到的所有参数，进行求和</span>
  echo array_sum($arr);  <span style="color: #008000;">//</span><span style="color: #008000;">这里输出结果值

  </span><span style="color: #008000;">//</span><span style="color: #008000;">获取当前参数的数量</span>
  $arr_len =<span style="color: #000000;"> func_num_args();
}</span></pre>
</div>
<p>&nbsp;</p>
<p>php5.5后</p>
<p>...xxx&nbsp; &nbsp;//获取所有传递过来的参数</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">function avg(...arr){
  print_r($arr); </span><span style="color: #008000;">//</span><span style="color: #008000;">这里会获取到所有传递过来的参数的数组</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>函数返回值</p>
<p>略。。。</p>
<p>&nbsp;</p>
<h2>回调函数</h2>
<p>callback回调函数是：作为参数，传进另一个函数中使用的函数</p>
<p>如：call_user_func('回调' , '参数')</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span> add (<span style="color: #800080;">$a</span><span style="color: #000000;">){
  </span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$a</span><span style="color: #000000;">;  
}

</span><span style="color: #008080;">call_user_func</span>('add','输出的内容'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">这样就会间接调用add函数</span></pre>
</div>
<p>&nbsp;</p>
<h2>递归函数</h2>
<p>递归函数：是指直接或间接调用函数本身的函数</p>
<p>递归函数条件：</p>
<p>1、在每一次调用自己时，必须是（在某种意义上）更接近于解</p>
<p>2、必须有一个终止处理或计算的准则</p>
<p>如：计算1-100的累加和</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span> recursive (<span style="color: #800080;">$n</span><span style="color: #000000;">){
  </span><span style="color: #0000ff;">if</span>(<span style="color: #800080;">$n</span> &gt;= 1<span style="color: #000000;">){
   </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">$n</span> + recursive(<span style="color: #800080;">$n</span> - 1<span style="color: #000000;">) ;      
  }  
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>可变函数</h2>
<p>可变函数：是指如果一个变量名后有圆括号，PHP将寻找与变量的值同名的函数，并尝试执行它</p>
<p>用途：可以用来实现包括回调函数，函数表在内的用途</p>
<p>注意：可变函数不能用于，echo、print、unset、isset、empty、include、require 以及类似的语言结构。</p>
<p>用可变函数的语法来调用一个对象的方法，如：</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$a</span> = '123'<span style="color: #000000;">;
</span><span style="color: #0000ff;">function</span> echoit(<span style="color: #800080;">$haha</span><span style="color: #000000;">){
    </span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$haha</span><span style="color: #000000;">;
}
</span><span style="color: #800080;">$c</span> = 'echoit'<span style="color: #000000;">;
</span><span style="color: #800080;">$c</span>(<span style="color: #800080;">$a</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;字符串函数</h2>
<p>strlen：获取字符串长度，如</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strlen</span>('hahaixixixi');</pre>
</div>
<p>&nbsp;</p>
<p>strtolower：将字符串转换为小写，如</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strtolower</span>('SDLFKJSLDKFLS');    </pre>
</div>
<p>strtoupper：将字符串转为大写，如</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strtoupper</span>('hahaixixixi');</pre>
</div>
<p>&nbsp;</p>
<p>ucfirst：将句子首字母转换为大写，如</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">ucfirst</span>('are you ok?');</pre>
</div>
<p>ucwords：将每个单词的首字母转换为大写，如　　</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">ucwords</span>('are you ok?');</pre>
</div>
<p>&nbsp;</p>
<p>str_replace：查找字符串中的字符，并进行替换，如</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">str_replace</span>('a','1','hahahaha');<span style="color: #008000;">//</span><span style="color: #008000;">查找字符串中的a，将a替换成1</span></pre>
</div>
<p>&nbsp;</p>
<p>htmlspecialchars：预定义字符转为 HTML 实体，如</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> $str = "&lt;h1&gt;转为实体&lt;/h1&gt;";
// $echoi = htmlspecialchars($str,ENT_COMPAT);//ENT_COMPAT仅编码双引号，默认
// echo $echoi;

// $str = '&lt;h1&gt;转为实体&lt;/h1&gt;';
// $echoi = htmlspecialchars($str,ENT_QUOTES);//ENT_QUOTES仅编码 双引号 和 单引号
// echo $echoi;</span>

<span style="color: #800080;">$str</span> = "&lt;h1&gt;转为实体&lt;/h1&gt;"<span style="color: #000000;">;
</span><span style="color: #800080;">$echoi</span> = <span style="color: #008080;">htmlspecialchars</span>(<span style="color: #800080;">$str</span>,ENT_NOQUOTES);<span style="color: #008000;">//</span><span style="color: #008000;">不编码任何引号</span>
<span style="color: #0000ff;">echo</span> <span style="color: #800080;">$echoi</span>;</pre>
</div>
<p>//即将单引号或双引号里面的，&amp; &gt; &lt; " ' 等转为html字符</p>
<p>&nbsp;</p>
<p>ltrim：实现删除字符串开始位置的空格或其他字符</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> $str = "Hello    World!";
// echo $str . "&lt;br&gt;";
// echo ltrim($str,"Hello");//从字符串左边，截取Hello，返回截取后的结果

//若第二个参数省略，则去除以下所有字符
// "\0" - NULL
// "\t" - 制表符
// "\n" - 换行
// "\x0B" - 垂直制表符
// "\r" - 回车
// " " - 空格</span>
<span style="color: #800080;">$str</span> = " \0     HelloWorld!"<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">ltrim</span>(<span style="color: #800080;">$str</span>);</pre>
</div>
<p>&nbsp;rtrim：实现删除字符串结束位置的空格或其他字符</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> $str = "Hello    World!";
// echo $str . "&lt;br&gt;";
// echo ltrim($str,"World");//从字符串右边，截取World，返回截取后的结果

//若第二个参数省略，则去除以下所有字符
// "\0" - NULL
// "\t" - 制表符
// "\n" - 换行
// "\x0B" - 垂直制表符
// "\r" - 回车
// " " - 空格</span>
<span style="color: #800080;">$str</span> = "Hello World!\0    "<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">ltrim</span>(<span style="color: #800080;">$str</span>);</pre>
</div>
<p>&nbsp;trim：实现删除字符串 开始和结束位置 的空格和其他字符</p>
<p>&nbsp;</p>
<p>strpos：返回一个字符出现在另一个字符串，第一次出现的位置</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strpos</span>('lksdjlkasdkf','a'); <span style="color: #008000;">//7  </span><span style="color: #008000;">返回a在字符串里面第一次出现的位置</span></pre>
</div>
<p>stripos：返回一个字符出现在另一个字符串，第一次出现的位置，忽略大小写</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strpos</span>('lksdjlkAsdkf','a'); <span style="color: #008000;">//7  </span><span style="color: #008000;">返回a在字符串里面第一次出现的位置，忽略大小写</span></pre>
</div>
<p>&nbsp;</p>
<p>strrpos：返回一个字符在另一个字符串，最后一次出现的位置</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strrpos</span>('lksdjlkasdkfa','a'); <span style="color: #008000;">//</span><span style="color: #008000;">12  返回a在字符串里面，最后一次出现的位置</span></pre>
</div>
<p>&nbsp;strrpos：返回一个字符在另一个字符串，最后一次出现的位置，忽略大小写</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strrpos</span>('lksdjlkasdkfA','a'); <span style="color: #008000;">//</span><span style="color: #008000;">12  返回a在字符串里面，最后一次出现的位置，忽略大小写</span></pre>
</div>
<p>&nbsp;</p>
<p>explode：字符串转数组</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$str</span> = 'a|b|c|d'<span style="color: #000000;">;
</span><span style="color: #008080;">print_r</span>(<span style="color: #008080;">explode</span>('|' , <span style="color: #800080;">$str</span>)); //以 | 为分界线进行分割</pre>
</div>
<p>implode：将数组转为字符串</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = <span style="color: #0000ff;">array</span>('a' , 'b' , 'c' , 'd'<span style="color: #000000;">);
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">implode</span>(<span style="color: #800080;">$arr</span>); <span style="color: #008000;">//</span><span style="color: #008000;">将数组每一项拼接起来，没有分隔</span>
<span style="color: #0000ff;">echo</span> '&lt;br&gt;'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">implode</span>(',' , <span style="color: #800080;">$arr</span>); <span style="color: #008000;">//</span><span style="color: #008000;">将数组每一项拼接起来，用逗号分隔</span></pre>
</div>
<p>&nbsp;</p>
<p>substr：截取字符串</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$str</span> = 'abcdefg'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">substr</span>(<span style="color: #800080;">$str</span> , 0 , 2);<span style="color: #008000;">//</span><span style="color: #008000;">从第0为开始，截取长度为2，若长度为负数，则往回截取</span>
<span style="color: #0000ff;">echo</span> '&lt;br&gt;'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">substr</span>(<span style="color: #800080;">$str</span> , 0); <span style="color: #008000;">//</span><span style="color: #008000;">若省略长度，则截取到最后一位</span></pre>
</div>
<p>&nbsp;</p>
<p>strstr：将搜索一个字符串在另一个字符串中第一次出现的位置，区分大小写。返回字符串的其余部分</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$str1</span> = 'abcdefg'<span style="color: #000000;">;
</span><span style="color: #800080;">$str2</span> = 'c'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strstr</span>(<span style="color: #800080;">$str1</span> , <span style="color: #800080;">$str2</span>); <span style="color: #008000;">//</span><span style="color: #008000;">将返回str2第一次出现的位置，直到最后。即cdefg</span></pre>
</div>
<p>stristr：将搜索一个字符串在另一个字符串中第一次出现的位置，不区分大小写。返回字符串的其余部分</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$str1</span> = 'abcdefg'<span style="color: #000000;">;
</span><span style="color: #800080;">$str2</span> = 'C'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">strstr</span>(<span style="color: #800080;">$str1</span> , <span style="color: #800080;">$str2</span>); <span style="color: #008000;">//</span><span style="color: #008000;">将返回str2第一次出现的位置，直到最后。即cdefg</span></pre>
</div>
<p>&nbsp;</p>
<p>md5：字符串加密，或者说计算字符串的md5的哈希值</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$str</span>  = 'hahaha'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">md5</span>(<span style="color: #800080;">$str</span>);</pre>
</div>
<p>&nbsp;</p>
<p>str_shuffle：随机打乱字符串</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$str</span> = 'aslkjfsldfklsdf'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">str_shuffle</span>(<span style="color: #800080;">$str</span>);</pre>
</div>
<p>&nbsp;</p>
<p>sprintf：字符串格式函数</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$num</span> = 5<span style="color: #000000;">;
</span><span style="color: #800080;">$str</span> = 'apple'<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">sprintf</span>(' there are %d %s ' , <span style="color: #800080;">$num</span>,<span style="color: #800080;">$str</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">若一个只有一个变量的话</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">sprintf</span>(' there are %1d  and %1d ',<span style="color: #800080;">$num</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">若设置小数点长度</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">sprintf</span>(' there are %.2f ',<span style="color: #800080;">$num</span>);</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">规定字符串以及如何格式化其中的变量</span>
%%  <span style="color: #008000;">//</span><span style="color: #008000;">返回一个百分号%</span>
%b   <span style="color: #008000;">//</span><span style="color: #008000;">二进制数</span>
%d   <span style="color: #008000;">//</span><span style="color: #008000;">包含正负号的十进制数</span>
%e   <span style="color: #008000;">//</span><span style="color: #008000;">使用小写的科学计数法（例如 1.2e+2）</span>
%s   <span style="color: #008000;">//</span><span style="color: #008000;">字符串</span>
%f   <span style="color: #008000;">//</span><span style="color: #008000;">浮点数（本地设置）</span>

 . <span style="color: #008000;">//</span><span style="color: #008000;">附加的格式值，必须放置在%和字母之间（例如%.2f）</span>
 + - <span style="color: #008000;">//</span><span style="color: #008000;">在数字前面加上 + 或 - 来定义数字的正负性。只有负数才做标记，正数不做标记</span>
 -'<span style="color: #000000;"> //规定使用什么作为填充，默认是空格。它必须与宽度指定器一起使用
 -- //左调整变量值
 -[0-9] //规定变量的最小宽度
 -.[0-9] //规定小数位数或最大字符串长度 </span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>数学函数库</h2>
<p>ceil：向上取整</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$num</span> = 3.14<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">ceil</span>(<span style="color: #800080;">$num</span>); <span style="color: #008000;">//</span><span style="color: #008000;">输出4</span></pre>
</div>
<p>floor：向下取整</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$num</span> = 3.14<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">floor</span>(<span style="color: #800080;">$num</span>); <span style="color: #008000;">//</span><span style="color: #008000;">输出3</span></pre>
</div>
<p>round：四舍五入</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$n</span> = 3.14159<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">round</span>(<span style="color: #800080;">$n</span>); <span style="color: #008000;">//</span><span style="color: #008000;">3</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">round</span>(<span style="color: #800080;">$n</span> , 3); <span style="color: #008000;">//</span><span style="color: #008000;">3.142    取到小数点后3位</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;number_format：以千位分隔符方式，格式化数字</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$n</span> = 2348.456<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">number_format</span>(<span style="color: #800080;">$n</span>); <span style="color: #008000;">//</span><span style="color: #008000;">2,348</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">number_format</span>(<span style="color: #800080;">$n</span> , 2); <span style="color: #008000;">//</span><span style="color: #008000;">2,348.46    格式化到小数位后两位，附带四舍五入</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>pow：幂运算</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">pow</span>(2 , 3);  <span style="color: #008000;">//</span><span style="color: #008000;">8    2的3次方</span></pre>
</div>
<p>&nbsp;</p>
<p>sqrt：平方根</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">sqrt</span>(4); <span style="color: #008000;">//</span><span style="color: #008000;">2     4的平方根</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>rand：随机数</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">rand</span>(0,100); <span style="color: #008000;">//</span><span style="color: #008000;">输出0-100之间的随机数</span></pre>
</div>
<p>mt_rand：更好的随机数，速度比 rand 快3倍左右</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">mt_rand</span>(0-100); <span style="color: #008000;">//</span><span style="color: #008000;">输出0-100之间的随机数</span></pre>
</div>
<p>&nbsp;</p>
<p>fmod：浮点数余数</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">浮点数余数</span>
echo fmod(<span style="color: #800080;">7.8</span> , <span style="color: #800080;">3</span>); <span style="color: #008000;">//</span><span style="color: #008000;">1.8

</span><span style="color: #008000;">//</span><span style="color: #008000;">整数余数</span>
echo <span style="color: #800080;">7.8</span> % <span style="color: #800080;">3</span>; <span style="color: #008000;">//</span><span style="color: #008000;">1 </span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;max：获取两个或以上数字的最大值</p>
<div class="cnblogs_code">
<pre>$x = <span style="color: #800080;">3</span><span style="color: #000000;">;
$y </span>= <span style="color: #800080;">7</span><span style="color: #000000;">;
$z </span>= <span style="color: #800080;">8.8</span><span style="color: #000000;">;
echo max($x,$y,$z); </span><span style="color: #008000;">//</span><span style="color: #008000;">8.8</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;min：获取两个或以上数字的最小值</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$x</span> = 3<span style="color: #000000;">;
</span><span style="color: #800080;">$y</span> = 7<span style="color: #000000;">;
</span><span style="color: #800080;">$z</span> = 8.8<span style="color: #000000;">;
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">min</span>(<span style="color: #800080;">$x</span>,<span style="color: #800080;">$y</span>,<span style="color: #800080;">$z</span>); <span style="color: #008000;">//</span><span style="color: #008000;">3</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;日期时间函数库</h2>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202009/1680452-20200905153038960-9173072.png" alt="" width="744" height="222" loading="lazy" /></p>
<h3>配置文件修改时区</h3>
<p>1、php.ini 中查找Date</p>
<p>2、将 date.timezone 前的分号去掉</p>
<p>3、在 date.timezone = 后面加上 'Asia/Shanghai'</p>
<p>4、 重启Apachech服务器</p>
<h3>PHP函数修改时区</h3>
<div class="cnblogs_code">
<pre>date_default_timezone_set('Asia/Shanghai');</pre>
</div>
<p>&nbsp;</p>
<h3>获取当前时区</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> date_default_timezone_get();</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>函数操作</h3>
<p>date：格式化本地时间 / 日期</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">date</span>('Y年m月d日 , H:i:s');<br /><br />echo '昨天这个时候的时间是' . date('Y-m-d H:i:s' , time()-86400);  //将时间戳转为正常时间</pre>
<pre>echo date('Y-m-d H:i:s' , 23423434...); //将时间戳转为正常时间</pre>
</div>
<p>&nbsp;</p>
<p>strtotime：将字符串转Unix时间戳，即精确计算某个时间点的时间戳</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> '三个星期之前的时间戳为' , <span style="color: #008080;">strtotime</span>('-3 weeks');<br />echo '上个月的第一天的时间戳为' , strtotime('last day of -1 month'); //不能直接用 -1 month，因为 -1 month 是以30天为单位计算的</pre>
</div>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202009/1680452-20200905161939673-1892534350.png" alt="" width="922" height="283" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/1680452/202009/1680452-20200905162100539-1130301819.png" alt="" width="299" height="287" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;microtime：返回 unix 时间戳和微秒数</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">microtime</span>(); <span style="color: #008000;">//</span><span style="color: #008000;">返回当前的微秒数 及时间戳，空格隔开</span>

<span style="color: #0000ff;">echo</span> <span style="color: #008080;">microtime</span>(<span style="color: #0000ff;">true</span>); <span style="color: #008000;">//</span><span style="color: #008000;">返回当前时间戳，含微秒数</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>uniqid：生成唯一的id号</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">echo</span> <span style="color: #008080;">uniqid</span>(); <span style="color: #008000;">//</span><span style="color: #008000;">唯一id号</span>

<span style="color: #0000ff;">echo</span> <span style="color: #008080;">uniqid</span>('haha'); <span style="color: #008000;">//</span><span style="color: #008000;">给id号加前缀 haha</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>getdate：获取当前时间的信息，数组形式返回</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">print_r</span>( <span style="color: #008080;">getdate</span>() );</pre>
</div>
<p>&nbsp;</p>
