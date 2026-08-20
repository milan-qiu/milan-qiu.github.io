---
title: "03、PHP数组"
date: "2020-12-18 13:05:00"
tags:
categories:
description: >-
  数组定义 数组是php中的重要数据类型之一，是复合类型。数组的集合，在php中数组是一个有序映射 数组分类 索引数组：数组的下标是数字 关联数组：数组的下标是字符 注：php中数组其实是不区分索引还是关联数组，都是根据键名找键值。 数组定义 一、通过 array() 形式创建 $arr = arra
---

<h3>数组定义</h3>
<p>数组是php中的重要数据类型之一，是复合类型。数组的集合，在php中数组是一个有序映射</p>
<h3>数组分类</h3>
<p>索引数组：数组的下标是数字</p>
<p>关联数组：数组的下标是字符</p>
<p>注：php中数组其实是不区分索引还是关联数组，都是根据键名找键值。</p>
<h3>数组定义</h3>
<p>一、通过 array() 形式创建</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = <span style="color: #0000ff;">array</span>();<br /><br />$arr1 = array(1,'dkf',45); //索引数组<br /><br />$arr2 = array('first' =&gt; 'first_value' , 4 =&gt; 'secend_value'); //关联数组 + 索引 = 混合</pre>
</div>
<p>&nbsp;</p>
<p>二、通过 [ ] 形式创建</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> =<span style="color: #000000;"> [];
$arr[] = 'haha';<br />$arr[] = 234;<br />$arr['haha'] = 'haha';<br />
</span><span style="color: #800080;">$arr1</span> = ['asd','df',34]; <span style="color: #008000;">//</span><span style="color: #008000;">索引数组</span>

<span style="color: #800080;">$arr2</span> =<span style="color: #000000;"> [
    </span>'user' =&gt; 'zhang',
    'haha' =&gt; 'haha'<span style="color: #000000;">
];</span></pre>
</div>
<p>&nbsp;</p>
<p>三、通过 range() 和 compact() 创建</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">range</span>()  <span style="color: #008000;">//</span><span style="color: #008000;">快速创建索引数组</span>
<span style="color: #800080;">$arr</span> = <span style="color: #008080;">range</span>(3,13); <span style="color: #008000;">//</span><span style="color: #008000;">创建数组，值从3开始，一直到13结束</span>
<span style="color: #800080;">$arr1</span> = <span style="color: #008080;">range</span>(3,13,2); <span style="color: #008000;">//</span><span style="color: #008000;">第三个参数是步长，原来每次加1，现在每次加2</span>
<span style="color: #800080;">$arr2</span> = <span style="color: #008080;">range</span>('a','z');<br /><br />compact()  //快速将变量转换为数组，针对已有变量<br />$username = 'zhang';<br />$email = '234@163.com';<br />$age = 18;<br />$arr = compact('username','email','age'); //字符串里面为变量名</pre>
</div>
<p>&nbsp;</p>
<p>四、通过 define() 定义常量数组</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">const定义数组
</span><span style="color: #0000ff;">const</span> ARR = <span style="color: #0000ff;">array</span>(1,23,4<span style="color: #000000;">);
</span><span style="color: #0000ff;">const</span> ARR2 = [1,2,3<span style="color: #000000;">];

define定义数组
</span><span style="color: #008080;">define</span>('ARR3' , [2,3,4,5<span style="color: #000000;">]);
</span><span style="color: #008080;">define</span>('ARR4' , <span style="color: #0000ff;">array</span>(2,3,4));</pre>
</div>
<p>&nbsp;</p>
<h3>检测是否为数组</h3>
<div class="cnblogs_code">
<pre><span style="color: #008080;">var_dump</span>(<span style="color: #800080;">$arr</span>); <span style="color: #008000;">//</span><span style="color: #008000;">返回类型及数据</span>

<span style="color: #0000ff;">echo</span> <span style="color: #008080;">gettype</span>(<span style="color: #800080;">$arr</span>); <span style="color: #008000;">//</span><span style="color: #008000;">返回类型名称</span>

<span style="color: #008080;">var_dump</span>(<span style="color: #008080;">is_array</span>(<span style="color: #800080;">$arr</span>));<span style="color: #008000;">//</span><span style="color: #008000;">返回boolean</span></pre>
</div>
<p>&nbsp;</p>
<h3>二维数组</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">数组里面包含数组就是二维数组。数组+数组+数组 = 三维数组 ......</span>

<span style="color: #800080;">$arr</span> = <span style="color: #0000ff;">array</span>(   <span style="color: #008000;">//</span><span style="color: #008000;">索引包索引</span>
   <span style="color: #0000ff;">array</span>(1,2,3),
   <span style="color: #0000ff;">array</span>(4,5,6<span style="color: #000000;">)  
);
</span><span style="color: #800080;">$arr1</span> = <span style="color: #0000ff;">array</span>(   <span style="color: #008000;">//</span><span style="color: #008000;">索引包关联</span>
   <span style="color: #0000ff;">array</span><span style="color: #000000;">(</span>'name' = 'haha','age' = 18<span style="color: #000000;">)</span>, 
   <span style="color: #0000ff;">array</span><span style="color: #000000;">(</span>'name' = 'haha','age' = 18<span style="color: #000000;">)</span><span style="color: #000000;">
);
</span><span style="color: #800080;">$arr2</span> = <span style="color: #0000ff;">array</span>(   <span style="color: #008000;">//</span><span style="color: #008000;">关联包索引</span>
    'users' =&gt; <span style="color: #0000ff;">array</span>(1,2,3),
    'ages' =&gt; <span style="color: #0000ff;">array</span>(4,5,6<span style="color: #000000;">)
);
</span><span style="color: #800080;">$arr3</span> = <span style="color: #0000ff;">array</span>(   <span style="color: #008000;">//</span><span style="color: #008000;">关联包关联</span>
    'users' =&gt; <span style="color: #0000ff;">array</span>('username' =&gt; 'haha'),
    'ages' =&gt; <span style="color: #0000ff;">array</span>('age' =&gt; 15<span style="color: #000000;">)
);<br /><br />//同样可以用 [] 来创建</span></pre>
</div>
<p>&nbsp;</p>
<h3>数组增删改查</h3>
<p>查</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [2,3,4,2,4<span style="color: #000000;">];
</span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$arr</span>[2]; <span style="color: #008000;">//</span><span style="color: #008000;">数组下标为2的值</span>

<span style="color: #800080;">$arr1</span> = ['name' =&gt; 'haha' , 'age' =&gt; 18<span style="color: #000000;">];
</span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$arr1</span>['name']; <span style="color: #008000;">//</span><span style="color: #008000;">输出数组索引为name的值<br /><br />$arr2 = [12 , ['name'=&gt;'qiu' , 'age'=&gt;18]]<br />echo $arr2[1]['name'];<br />echo $arr2[1]{'name'}; //可以使用花括号，效果一样</span></pre>
</div>
<p>增</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [1,2<span style="color: #000000;">];
</span><span style="color: #800080;">$arr</span>[] = 3<span style="color: #000000;">;
</span><span style="color: #800080;">$arr</span>['name'] = 'qiu';</pre>
</div>
<p>改</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [1,2,2,2<span style="color: #000000;">];
</span><span style="color: #800080;">$arr</span>[0] = 2;</pre>
</div>
<p>删</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [1,2,3,4,'name'=&gt;'qiu'<span style="color: #000000;">];
</span><span style="color: #0000ff;">unset</span>(<span style="color: #800080;">$arr</span>['name'<span style="color: #000000;">]);
</span><span style="color: #0000ff;">unset</span>(<span style="color: #800080;">$arr</span>[0]);</pre>
</div>
<p>&nbsp;</p>
<h3>数组运算符</h3>
<p>+&nbsp; &nbsp; //合并数组</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr1</span> = [1,2<span style="color: #000000;">];
</span><span style="color: #800080;">$arr2</span> = [3,4<span style="color: #000000;">];
</span><span style="color: #800080;">$new_arr</span>= <span style="color: #800080;">$arr1</span> + <span style="color: #800080;">$arr2</span>; <span style="color: #008000;">//</span><span style="color: #008000;">若索引相同，只回采用+号左边的，并不会覆盖。所以结果还是 [1,2]<br /><br />$arr3 = $arr1 +['name'=&gt;'haha','age'=&gt;19];  //这样就会合并起来</span></pre>
</div>
<p>&nbsp;</p>
<p>==&nbsp; &nbsp;//判断数组是否相同，顺序可以错乱，还会进行类型转换</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$a</span> = ['45' =&gt; 234<span style="color: #000000;">];
</span><span style="color: #800080;">$b</span> = [45 =&gt; '234'<span style="color: #000000;">];
</span><span style="color: #008080;">var_dump</span>(<span style="color: #800080;">$a</span> == <span style="color: #800080;">$b</span>); <span style="color: #008000;">//</span><span style="color: #008000;">true</span></pre>
</div>
<p>&nbsp;</p>
<p>===&nbsp; &nbsp;//判断数组是否相同，顺序要相同，类型也必须相同</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$a</span> = ['45' =&gt; 234<span style="color: #000000;">];
</span><span style="color: #800080;">$b</span> = [45 =&gt; '234'<span style="color: #000000;">];
</span><span style="color: #008080;">var_dump</span>(<span style="color: #800080;">$a</span> == <span style="color: #800080;">$b</span>); <span style="color: #008000;">//</span><span style="color: #008000;">false</span></pre>
</div>
<p>!=&nbsp; 是&nbsp; ==&nbsp; 的取反</p>
<p>!==&nbsp; 是&nbsp; ===&nbsp; 的取反</p>
<p>&nbsp;</p>
<h3>其他类型转换为数组</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">临时转换</span>
<span style="color: #800080;">$a</span> = 123<span style="color: #000000;">;
</span><span style="color: #800080;">$arr1</span> = (<span style="color: #0000ff;">array</span>)<span style="color: #800080;">$a</span><span style="color: #000000;">; 

</span><span style="color: #800080;">$b</span> = 'haha'<span style="color: #000000;">;
</span><span style="color: #800080;">$arr2</span> = (<span style="color: #0000ff;">array</span>)<span style="color: #800080;">$b</span><span style="color: #000000;">;

</span><span style="color: #800080;">$c</span> = <span style="color: #0000ff;">null</span><span style="color: #000000;">;
</span><span style="color: #800080;">$arr3</span> = (<span style="color: #0000ff;">array</span>)<span style="color: #800080;">$arr3</span>; <span style="color: #008000;">//</span><span style="color: #008000;">这里会转为空数组

//永久转换</span>
<span style="color: #008080;">settype</span>(<span style="color: #800080;">$a</span> , 'array'<span style="color: #000000;">);
</span><span style="color: #008080;">settype</span>(<span style="color: #800080;">$b</span> , ''<span style="color: #0000ff;">array</span><span style="color: #000000;">);
</span><span style="color: #008080;">settype</span>(<span style="color: #800080;">$c</span> , 'array'); <span style="color: #008000;">//</span><span style="color: #008000;">这里也是空数组，转换规则跟临时转换一样</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>计算数组的个数</h3>
<div class="cnblogs_code">
<pre><span style="color: #008080;">count</span>  <span style="color: #008000;">//</span><span style="color: #008000;">数组个数</span>

<span style="color: #800080;">$arr</span> = [1,2,3,4<span style="color: #000000;">];
</span><span style="color: #0000ff;">echo</span> <span style="color: #008080;">count</span>(<span style="color: #800080;">$arr</span>);  <span style="color: #008000;">//</span><span style="color: #008000;">4</span>

<span style="color: #0000ff;">echo</span> <span style="color: #008080;">count</span>('123'); <span style="color: #008000;">//</span><span style="color: #008000;">若传的是字符串，返回的是1</span>
<span style="color: #0000ff;">echo</span> <span style="color: #008080;">count</span>(<span style="color: #0000ff;">null</span>);  <span style="color: #008000;">//</span><span style="color: #008000;">若传的是null，返回的是0</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>foreach遍历数组</h3>
<p><em>foreach只能遍历数组或对象，否则会报错</em></p>
<p>foreach遍历一维数组</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [1,2,3,4,5,6<span style="color: #000000;">];

</span><span style="color: #0000ff;">foreach</span>(<span style="color: #800080;">$arr</span> <span style="color: #0000ff;">as</span> <span style="color: #800080;">$v</span><span style="color: #000000;">){
  </span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$y</span>;  <span style="color: #008000;">//</span><span style="color: #008000;">这里遍历出的是键值  </span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">foreach</span>(<span style="color: #800080;">$arr</span> <span style="color: #0000ff;">as</span> <span style="color: #800080;">$k</span> =&gt; <span style="color: #800080;">$v</span><span style="color: #000000;">){
  </span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$k</span>,<span style="color: #800080;">$v</span>;  <span style="color: #008000;">//</span><span style="color: #008000;">这里输出的是键名 和 键值  </span>
}</pre>
</div>
<p>&nbsp;</p>
<p>foreach遍历二维数组</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [[1,2,3] , [,4,5,6<span style="color: #000000;">]];

</span><span style="color: #0000ff;">foreach</span>(<span style="color: #800080;">$arr</span> <span style="color: #0000ff;">as</span> <span style="color: #800080;">$v</span><span style="color: #000000;">){
  </span><span style="color: #0000ff;">foreach</span>(<span style="color: #800080;">$v</span> <span style="color: #0000ff;">as</span> <span style="color: #800080;">$val</span><span style="color: #000000;">){
     </span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$val</span><span style="color: #000000;">; 
  }  
}</span></pre>
</div>
<p>&nbsp;</p>
<p>可以通过 : 和 endforeach 代替 { }</p>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [1,2,3,4<span style="color: #000000;">];

</span><span style="color: #0000ff;">foreach</span>(<span style="color: #800080;">$arr</span> <span style="color: #0000ff;">as</span> <span style="color: #800080;">$v</span>):
    <span style="color: #0000ff;">echo</span> <span style="color: #800080;">$v</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">endforeach</span>;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>数组指针相关函数</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">数组默认指针，指向第一个元素</span>

<span style="color: #008080;">key</span>(<span style="color: #800080;">$arr</span>)  <span style="color: #008000;">//</span><span style="color: #008000;">得到当前指针所在的键名，没有则返回 null</span>
<span style="color: #008080;">current</span>(<span style="color: #800080;">$arr</span>)  <span style="color: #008000;">//</span><span style="color: #008000;">得到当前指针所在的键值，没有则返回false</span>

<span style="color: #008080;">next</span>(<span style="color: #800080;">$arr</span>)  <span style="color: #008000;">//</span><span style="color: #008000;">指针往下移动一位，并得到该位置的值，没有则返回false</span>
<span style="color: #008080;">prev</span>(<span style="color: #800080;">$arr</span>)  <span style="color: #008000;">//</span><span style="color: #008000;">指针往上移动一位，并得到该位置的值，没有则返回false<br /><br />reset($arr)  //指针移动到数组开始，并返回当前位置的值，没有则返回false<br />end($arr)   //指针移动到数组末尾，并返回当前位置的值，没有则返回false</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>指针函数遍历数组</h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> =<span style="color: #000000;"> [
   </span>'' =&gt; 'a',
   'a'=&gt;'b', 
   <span style="color: #0000ff;">null</span>=&gt;'c'<span style="color: #000000;">
];

</span><span style="color: #008000;">//</span><span style="color: #008000;">根据key来遍历数组</span>
<span style="color: #0000ff;">while</span>(!<span style="color: #008080;">is_null</span>(<span style="color: #800080;">$arr</span><span style="color: #000000;">)){
  </span><span style="color: #0000ff;">echo</span> '当前键名'.<span style="color: #008080;">key</span>(<span style="color: #800080;">$arr</span>).'  当前键值'.<span style="color: #008080;">current</span>(<span style="color: #800080;">$arr</span><span style="color: #000000;">);
  </span><span style="color: #008080;">next</span>(<span style="color: #800080;">$arr</span>);  <span style="color: #008000;">//</span><span style="color: #008000;">将指针往后移动一位</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;">不能根据current来遍历，因为当键值存在0或false之类就会退出循环

//实用场景，获取文件扩展名</span>
<span style="color: #800080;">$file_name</span> = 'haha.php'<span style="color: #000000;">;
</span><span style="color: #800080;">$res</span> = <span style="color: #008080;">explode</span>('.' , <span style="color: #800080;">$file_name</span><span style="color: #000000;">);
</span><span style="color: #800080;">$ext</span> = <span style="color: #008080;">end</span>(<span style="color: #800080;">$res</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>list函数</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">list</span>  <span style="color: #008000;">//</span><span style="color: #008000;">把数组中的值赋给一些变量</span>

<span style="color: #800080;">$arr</span> = [1,2,3<span style="color: #000000;">];

</span><span style="color: #0000ff;">list</span>(,<span style="color: #800080;">$b</span>,) = <span style="color: #800080;">$arr</span>; <span style="color: #008000;">//</span><span style="color: #008000;">这样 $b 就得到了2</span>

<span style="color: #0000ff;">list</span>(<span style="color: #800080;">$a</span>,,<span style="color: #800080;">$c</span>) = <span style="color: #800080;">$arr</span>;  <span style="color: #008000;">//</span><span style="color: #008000;">这样 $a,$c 就得到了1,3</span>

<span style="color: #0000ff;">echo</span> <span style="color: #800080;">$a</span>,<span style="color: #800080;">$b</span>,<span style="color: #800080;">$c</span><span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">实用场景</span>
<span style="color: #800080;">$arr</span> = [ [1,2,3],[4,5,6],[7,8,9<span style="color: #000000;">] ];
</span><span style="color: #0000ff;">foreach</span>(<span style="color: #800080;">$arr</span> <span style="color: #0000ff;">as</span> <span style="color: #0000ff;">list</span>(<span style="color: #800080;">$a</span>,<span style="color: #800080;">$b</span>,<span style="color: #800080;">$c</span><span style="color: #000000;">)){
  </span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$a</span>,<span style="color: #800080;">$b</span>,<span style="color: #800080;">$c</span><span style="color: #000000;">; 
}</span></pre>
</div>
<p>&nbsp;</p>
<h3><span style="text-decoration: line-through;">each函数（即将弃用）</span></h3>
<div class="cnblogs_code">
<pre><span style="color: #008080;">each</span>  <span style="color: #008000;">//</span><span style="color: #008000;">返回数组当前指针的键值对数组，并将数组指针往前移动一步
//键值对数组：0为键，1为值，key为键，value为值。 一共4项</span>

<span style="color: #800080;">$arr</span> = [1,2,3<span style="color: #000000;">];
</span><span style="color: #008080;">print_r</span>(<span style="color: #008080;">each</span>(<span style="color: #800080;">$arr</span>)); <span style="color: #008000;">//</span><span style="color: #008000;">打印出第一项的数组</span></pre>
</div>
<p>&nbsp;</p>
<h3><span style="text-decoration: line-through;">list和each遍历数组（即将弃用）</span></h3>
<div class="cnblogs_code">
<pre><span style="color: #800080;">$arr</span> = [1,2,3<span style="color: #000000;">];

</span><span style="color: #0000ff;">while</span>(<span style="color: #0000ff;">list</span>(<span style="color: #800080;">$k</span>,<span style="color: #800080;">$v</span>) = <span style="color: #008080;">each</span>(<span style="color: #800080;">$arr</span><span style="color: #000000;">)){
  </span><span style="color: #0000ff;">echo</span> <span style="color: #800080;">$k</span>,<span style="color: #800080;">$v</span><span style="color: #000000;">;  
}</span></pre>
</div>
<p>&nbsp;</p>
