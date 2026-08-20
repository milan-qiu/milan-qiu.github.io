---
title: "6、Blade模板"
date: "2020-06-10 17:27:00"
tags:
categories:
description: >-
  模板继承 1、@section：定义了视图的一部分 //父模板定义： @session('se') 这是父模板搞得视图片段 @show //子模版继承： @session('ss') @stop //若子模版定义自己得内容 @session('ss') @parent <P> 这是子模版额外得内容
---

<h2>模板继承</h2>
<p>1、@section：定义了视图的一部分</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">父模板定义：</span>
@session(<span style="color: #800000;">'</span><span style="color: #800000;">se</span><span style="color: #800000;">'</span><span style="color: #000000;">)
这是父模板搞得视图片段
@show

</span><span style="color: #008000;">//</span><span style="color: #008000;">子模版继承：</span>
@session(<span style="color: #800000;">'</span><span style="color: #800000;">ss</span><span style="color: #800000;">'</span><span style="color: #000000;">)
@stop
</span><span style="color: #008000;">//</span><span style="color: #008000;">若子模版定义自己得内容</span>
@session(<span style="color: #800000;">'</span><span style="color: #800000;">ss</span><span style="color: #800000;">'</span><span style="color: #000000;">)
    @parent
    </span>&lt;P&gt; 这是子模版额外得内容 &lt;/p&gt;<span style="color: #000000;">
@stop</span></pre>
</div>
<p>&nbsp;</p>
<p>2、@yield：用来显示指定部分内容</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">父模板定义：</span>
&lt;title&gt; 父标题 - @yield(<span style="color: #800000;">'</span><span style="color: #800000;">title</span><span style="color: #800000;">'</span>) &lt;/title&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">子模版继承：</span>
@session(<span style="color: #800000;">'</span><span style="color: #800000;">title</span><span style="color: #800000;">'</span> , <span style="color: #800000;">'</span><span style="color: #800000;">child</span><span style="color: #800000;">'</span><span style="color: #000000;">)

</span><span style="color: #008000;">//</span><span style="color: #008000;">实际效果</span>
父标题 -<span style="color: #000000;"> child

</span><span style="color: #008000;">//</span><span style="color: #008000;">@yield即相当于占位符</span></pre>
</div>
<p>&nbsp;</p>
<p>3、@extends：继承模板的全部内容</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">父模板正常定义视图

</span><span style="color: #008000;">//</span><span style="color: #008000;">子模版继承：</span>
@extend(<span style="color: #800000;">'</span><span style="color: #800000;">layouts.blade</span><span style="color: #800000;">'</span><span style="color: #000000;">)

</span><span style="color: #008000;">//</span><span style="color: #008000;">继承父模板的全部视图</span></pre>
</div>
<p>&nbsp;</p>
<p>4、@parent：除了继承公共部分外，还有自己独立的数据</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">父模板用session定义视图</span>
@section(<span style="color: #800000;">'</span><span style="color: #800000;">name1</span><span style="color: #800000;">'</span><span style="color: #000000;">)
父视图
@show

</span><span style="color: #008000;">//</span><span style="color: #008000;">子模版继承的同时，添加自己的数据</span>
@section(<span style="color: #800000;">'</span><span style="color: #800000;">name1</span><span style="color: #800000;">'</span><span style="color: #000000;">)
    @parent
    子模版自己的内容
@stop</span></pre>
</div>
<p>&nbsp;</p>
<p>一、在view下新建 公共模板：xx.blade.php</p>
<p>二、子模板不论在view下的那个地方，@extends都可以写：@extends('xx')</p>
<p>&nbsp;</p>
<h2>基础语法及include的使用</h2>
<p>1、模板中输出变量</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">控制器 向 视图 传 变量</span>
$name = <span style="color: #800000;">"</span><span style="color: #800000;">张张</span><span style="color: #800000;">"</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">return</span> view(<span style="color: #800000;">'</span><span style="color: #800000;">bb</span><span style="color: #800000;">'</span><span style="color: #000000;">,[
    </span><span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> $name
]);
</span><span style="color: #008000;">//</span><span style="color: #008000;">给视图传 $name

</span><span style="color: #008000;">//</span><span style="color: #008000;">视图接收变量，并输出</span>
{{ $name }}</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>2、模板中调用php代码</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板中直接输出</span>
&lt;p&gt; {{ date(<span style="color: #800000;">'</span><span style="color: #800000;">Y-m-d H-i-s</span><span style="color: #800000;">'</span>,time()) }} &lt;/p&gt;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3、原样输出</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">若不想{{$name}}被解析，想要直接输出</span>
<span style="color: #000000;">@{{$name}}
</span><span style="color: #008000;">//</span><span style="color: #008000;">即可</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>4、模板中的注释</p>
<div class="cnblogs_code">
<pre>{{--  注释的内容  --<span style="color: #000000;">}}

</span><span style="color: #008000;">//</span><span style="color: #008000;">这里的内容在浏览器看不到</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>5、引入子视图include的使用</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">如：view下定义一个error.blade.php的视图</span>
&lt;p&gt; 错误信息&lt;/p&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">引入子视图</span>
@include(<span style="color: #800000;">'</span><span style="color: #800000;">error</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span><span style="color: #008000;">//</span><span style="color: #008000;">这样子视图的内容即被输出</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>模板中的流程控制</h2>
<p>1、if else</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">控制器向视图，传变量</span>
$name = <span style="color: #800000;">'</span><span style="color: #800000;">ming</span><span style="color: #800000;">'</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">return</span> view(<span style="color: #800000;">'</span><span style="color: #800000;">welcome</span><span style="color: #800000;">'</span> , [<span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> $name]);

</span><span style="color: #008000;">//</span><span style="color: #008000;">视图进行判断</span>
<span style="color: #000000;">
@if($name</span>==<span style="color: #800000;">'</span><span style="color: #800000;">ming</span><span style="color: #800000;">'</span><span style="color: #000000;">)
我是ming
@else($name</span>==<span style="color: #800000;">'</span><span style="color: #800000;">qiu</span><span style="color: #800000;">'</span><span style="color: #000000;">)
我是qiu
@endif

</span><span style="color: #008000;">//</span><span style="color: #008000;">if else 结尾处需要加 @endif</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>2、unless ：相当于if的取反</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">控制器传</span>
$name = <span style="color: #800000;">'</span><span style="color: #800000;">ming</span><span style="color: #800000;">'</span><span style="color: #000000;"> ;
</span><span style="color: #0000ff;">return</span> view(<span style="color: #800000;">'</span><span style="color: #800000;">bb</span><span style="color: #800000;">'</span>,[<span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span><span style="color: #000000;">,$name]);

</span><span style="color: #008000;">//</span><span style="color: #008000;">模板使用</span>
@unless( $name != <span style="color: #800000;">'</span><span style="color: #800000;">ming</span><span style="color: #800000;">'</span><span style="color: #000000;"> )
i am ming
@endunless</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3、for&nbsp;</p>
<div class="cnblogs_code">
<pre>@for( $i=<span style="color: #800080;">0</span>; $i&lt;<span style="color: #800080;">10</span>; $i++<span style="color: #000000;"> )
</span>&lt;p&gt; $i &lt;/p&gt;<span style="color: #000000;">
@endfor</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>4、foreach：遍历数组 或 对象</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">控制器返回给视图模型对象</span>
$students = Student::<span style="color: #0000ff;">get</span><span style="color: #000000;">();
</span><span style="color: #0000ff;">return</span> view(<span style="color: #800000;">'</span><span style="color: #800000;">/bb</span><span style="color: #800000;">'</span><span style="color: #000000;">,[
    </span><span style="color: #800000;">'</span><span style="color: #800000;">students</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> $student
]);

</span><span style="color: #008000;">//</span><span style="color: #008000;">视图遍历</span>
@foreach($students <span style="color: #0000ff;">as</span><span style="color: #000000;"> $student)
    {{ $student </span>-&gt;<span style="color: #000000;"> name }}
@foreach</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>5、forelse：同样可以遍历数组 或 对象</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">同样控制器向视图传值

</span><span style="color: #008000;">//</span><span style="color: #008000;">视图遍历</span>
@forelse($students <span style="color: #0000ff;">as</span><span style="color: #000000;"> $student)
    </span>&lt;p&gt; {{ $student -&gt; name }} &lt;/p&gt;<span style="color: #000000;">
@empty
    </span>&lt;p&gt; 这是空的 &lt;/p&gt;<span style="color: #000000;">
@endforelse

</span><span style="color: #008000;">//</span><span style="color: #008000;">有数据就遍历，没有数据就不遍历</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>模板中的url</h2>
<p>1、url()：通过路由的名称跳转url</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">添加路由</span>
Route::any(<span style="color: #800000;">'</span><span style="color: #800000;">url</span><span style="color: #800000;">'</span>,[<span style="color: #800000;">'</span><span style="color: #800000;">as</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">url</span><span style="color: #800000;">'</span> , <span style="color: #800000;">'</span><span style="color: #800000;">uses</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">XxxController@hello</span><span style="color: #800000;">'</span><span style="color: #000000;">]);

</span><span style="color: #008000;">//</span><span style="color: #008000;">在任意视图添加 a 链接</span>
&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">{{ url(url) }}</span><span style="color: #800000;">"</span>&gt; 这是链接 &lt;/a&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">url() 里面填路由的名称</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>2、action()：通过指定控制器/方法名跳转rul</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">任意视图添加</span>
&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">{{ action('XxxController@index') }}</span><span style="color: #800000;">"</span>&gt; 根据控制器@方法名跳转 &lt;/a&gt;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3、route()：通过路由的别名跳转url</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">路由别名跳转</span>
Route::any(<span style="color: #800000;">'</span><span style="color: #800000;">url</span><span style="color: #800000;">'</span>,[<span style="color: #800000;">'</span><span style="color: #800000;">as</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">aac</span><span style="color: #800000;">'</span> , <span style="color: #800000;">'</span><span style="color: #800000;">uses</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">XxxController@hello</span><span style="color: #800000;">'</span><span style="color: #000000;">]);

</span><span style="color: #008000;">//</span><span style="color: #008000;">视图</span>
&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">{{ route('aac') }}</span><span style="color: #800000;">"</span>&gt; 别名跳转 &lt;/a&gt;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>//一般使用 url() 或 route() 就好</p>
