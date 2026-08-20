---
title: "01、Sass基础"
date: "2020-04-03 23:11:00"
updated: "2020-04-15 13:19:00"
tags:
categories:
description: >-
  什么是Sass？ Sass是一种CSS的开发工具，提供了许多便利的写法，大大节省了设计者的时间，使得CSS的开发，变得简单和可维护。 安装Sass过程 一、安装Ruby（Windows） Ruby + Devkit 2.6.5-1（x64）地址： https://github.com/oneclic
---

<h2>什么是Sass？</h2>
<p>Sass是一种CSS的开发工具，提供了许多便利的写法，大大节省了设计者的时间，使得CSS的开发，变得简单和可维护。</p>
<p>&nbsp;</p>
<h2>安装Sass过程</h2>
<h3>一、安装Ruby（Windows）</h3>
<p>Ruby + Devkit 2.6.5-1（x64）地址： <a href="https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.5-1/rubyinstaller-devkit-2.6.5-1-x64.exe" target="_blank">https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.5-1/rubyinstaller-devkit-2.6.5-1-x64.exe</a><a class="downloadlink download-recommended" href="https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.5-1/rubyinstaller-devkit-2.6.5-1-x64.exe"><span><br /></span></a></p>
<p>&nbsp;</p>
<p>&nbsp;安装时除了更改路径外，其他都可以按照默认选项进行，直到安装完成的那个页面，把最后的勾去掉，如：</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202004/1680452-20200402220204824-824701610.jpg" alt="" width="418" height="323" /></p>
<p>&nbsp;</p>
<p>cmd进入控制台进行配置</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">查看是否安装成功</span>
ruby -<span style="color: #000000;">v

</span><span style="color: #008000;">//</span><span style="color: #008000;">如安装成功会打印</span>
ruby 2.6.5p114 (2019-10-01 revision 67812) [x64-<span style="color: #000000;">mingw32]

</span><span style="color: #008000;">//</span><span style="color: #008000;">尽可能更新RubyGems版本</span>
gem update --system <span style="color: #008000;">//</span><span style="color: #008000;">该命令请翻墙一下</span>

<span style="color: #008000;">//</span><span style="color: #008000;">更新后查看RubyGems版本</span>
gem -<span style="color: #000000;">v
</span><span style="color: #008000;">//</span><span style="color: #008000;">gem版本号</span>
3.0.3  

<span style="color: #008000;">//</span><span style="color: #008000;">删除替换原gem源</span>
gem sources --add https:<span style="color: #008000;">//</span><span style="color: #008000;">gems.ruby-china.com/ --remove https://rubygems.org/</span><span style="color: #008000;">
//</span><span style="color: #008000;">打印是否替换成功</span>
gem sources -<span style="color: #000000;">l
</span><span style="color: #008000;">//</span><span style="color: #008000;">确保只有 gems.ruby-china.com</span>
https:<span style="color: #008000;">//</span><span style="color: #008000;">gems.ruby-china.com </span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;二、安装Sass</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">Sass安装</span>
<span style="color: #000000;">gem install sass

</span><span style="color: #008000;">//</span><span style="color: #008000;">安装完之后查看版本，以确保安装成功</span>
sass -<span style="color: #000000;">v

</span><span style="color: #008000;">//</span><span style="color: #008000;">Sass常用命令</span>
gem update sass  <span style="color: #008000;">//</span><span style="color: #008000;">更新sass</span>
sass -v     <span style="color: #008000;">//</span><span style="color: #008000;">查看sass版本</span>
sass -h     <span style="color: #008000;">//</span><span style="color: #008000;">查看sass帮助</span></pre>
</div>
<p>&nbsp;</p>
<h3>三、安装Compass</h3>
<p>// compass 是一个 sass 的库，compass 里面有很多封装好的 mixin ，有了它，我们就可以很快的写出完美的，兼容的样式。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">安装compass</span>
<span style="color: #000000;">gem install compass

</span><span style="color: #008000;">//</span><span style="color: #008000;">安装完之后查看版本，以确保安装成功</span>
compass -v</pre>
</div>
<p>&nbsp;</p>
<h3>四、编译sass的方法</h3>
<p>CMD控制台</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">单文件转换命令</span>
<span style="color: #000000;">sass input.scss output.css

</span><span style="color: #008000;">//</span><span style="color: #008000;">单文件监听命令</span>
sass --<span style="color: #000000;">watch input.scss:output.css

</span><span style="color: #008000;">//</span><span style="color: #008000;">如果有很多sass文件的目录，可以监听整个目录</span>
sass --watch c:/baidu/bbb</pre>
</div>
<p>&nbsp;</p>
<p>Sublime Text插件</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">Sass Build 插件</span>
<span style="color: #000000;">
安装完成后，工具 </span>-&gt; 编译系统 -&gt;<span style="color: #000000;"> SASS

.scss 文件，ctrl</span>+s保存后，ctrl+<span style="color: #000000;">b编译，这时会在相同目录下，生成相同名字的.css 文件，还有同名的.css.map 文件。

如果：工具 </span>-&gt; 编译系统 -&gt; SASS -<span style="color: #000000;"> Compressed ,那么生成的代码就是压缩的.css 文件。

</span><span style="color: #008000;">//</span><span style="color: #008000;">SublimeOnSaveBuild 插件</span>
（按ctrl+s 就相当于：ctrl+s 和 ctrl+<span style="color: #000000;">b）

安装完成后，不需要配置，编写完.scss 文件，ctrl</span>+s 即可完成所需操作</pre>
</div>
<p>&nbsp;</p>
<p>VS Code插件：Live Sass Compiler</p>
<p>编译软件Koala：<a href="https://www.sass.hk/skill/koala-app.html">https://www.sass.hk/skill/koala-app.html</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>Sass基本语法</h2>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">变量名以$开头</span>
<span style="color: #000000;">$width:300px;
$height:300px;

</span><span style="color: #008000;">//</span><span style="color: #008000;">在写属性值的时候可以引用变量</span>
<span style="color: #000000;">div{
    width: $width;
    height: $height;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">变量名相同，最后的会覆盖之前的</span>
<span style="color: #000000;">$color:black;
$color:purple;

</span><span style="color: #008000;">//</span><span style="color: #008000;">!default表示默认的属性值</span>
$position:static !<span style="color: #0000ff;">default</span>;</pre>
</div>
<p>&nbsp;</p>
<p>字符串变量及拼接</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">变量可以是字符串</span>
$str:'xxx.jpg'<span style="color: #000000;">;
$class:</span>'.div'<span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">某些字符串可以不加引号</span>
<span style="color: #000000;">$string:abcdefg;

</span><span style="color: #008000;">//</span><span style="color: #008000;">引用字符串</span>
<span style="color: #000000;">.div{
    background</span>-image: url('./img/'+<span style="color: #000000;">$str);
}
</span><span style="color: #008000;">//插</span><span style="color: #008000;">值变量的方法引用字符串( #{} )</span>
<span style="color: #000000;">.div{
    background</span>-image: url('./img/#{$str}'<span style="color: #000000;">);
}
#{$class} {
    color: $color;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>变量作用域</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">全局作用域。在{}外面写，每个地方都可以引用</span>
<span style="color: #000000;">$width:100px;
.div{
    width: $width;
}
.bb{
    height: $width;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">局部作用域,{}内部定义只能内部使用</span>
<span style="color: #000000;">.div{
    $color:red;
    color: $color;
}
.bb{
    color: $color; </span><span style="color: #008000;">//</span><span style="color: #008000;">这样会报错，除非全局有$color</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>@import不需要编译</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">在sass文件中用@import，不会编译引入文件的情况（四种）<br /></span>
@import 'aa.css';   <span style="color: #008000;">//</span><span style="color: #008000;">以.css结尾</span>
@import 'http://www.qmlqmlqml.shop/bbc.scss'    <span style="color: #008000;">//</span><span style="color: #008000;">以http://开头，无论文件是scss还是css都不会编译</span>
@import 'url(bbc.css)';     <span style="color: #008000;">//</span><span style="color: #008000;">文件名是url()</span><span style="color: #008000;">
//</span><span style="color: #008000;">还有一种，@import 里面包含 media queries 的情况</span></pre>
</div>
<p>&nbsp;</p>
<p>@import需要编译，推荐的引入方式</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">引入的文件名以 _ 开头，文件扩展名 .scss/.sass ，如：</span>
<span style="color: #000000;">_demo.scss
</span><span style="color: #008000;">//</span><span style="color: #008000;">这样的好处就是，保存的时候不会单独地生成.css的文件，以koala软件为例</span>

<span style="color: #008000;">//</span><span style="color: #008000;">引入时，去掉 _ 和扩展名，如：</span>
@import 'demo';<br /><br />注意：不可以同时存在添加下划线 与 未添加下划线的 同名文件，添加下划线的文件将会被忽略</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>Sass基本数据类型</h2>
<p>number类型</p>
<div class="cnblogs_code">
<pre>$zoomValue = 3<span style="color: #000000;">;
.div{
    zoom:$zoomValue;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>color类型</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">$color:red;
$colour:#fe3232;
.div{
    background</span>-<span style="color: #000000;">color:$color;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>string类型</p>
<div class="cnblogs_code">
<pre>$str:'asdff.png'<span style="color: #000000;">
.div{
    background</span>-image:url('../shanghai/'+<span style="color: #000000;">$str);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>list类型（数组）</p>
<div class="cnblogs_code">
<pre>$list:(3,'ab'<span style="color: #000000;">,#fe3232,100px);
.div{
    color: nth($list,</span>3);  <span style="color: #008000;">//</span><span style="color: #008000;">获取数组下标为3的元素，下标从1开始，不是0</span>
    zoom:index($list,'ab'); <span style="color: #008000;">//</span><span style="color: #008000;">数组从头开始查找字符串'ab'，返回下标数字</span>
}</pre>
</div>
<p>&nbsp;</p>
<p>map类型（对象）</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">$map:(position:absolute,top:3px,right:3px,bottom:5px,left:5px);
.div{
    position:map</span>-get($map,position); <span style="color: #008000;">//</span><span style="color: #008000;">用map-get方法，获取$map里面的position属性</span>
    top:map-<span style="color: #000000;">get($map,top);
    left:map</span>-<span style="color: #000000;">get($map,left);
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">map类型的循环遍历</span>
<span style="color: #000000;">.div{
    @each $key,$value </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> $map{
        #{$key} : #{$value};    
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>算术运算</h2>
<h3>变量</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div{
    $num1:100px;
    $num2:200px;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">加</span>
    width: $num1 +<span style="color: #000000;"> $num2;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">减</span>
    height:$num2 -<span style="color: #000000;"> $num1;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">乘，这里变量只能乘数字，两个变量相乘会报错</span>
    margin:$num1*3<span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">除，这里只能乘数字</span>
    border:$num2/25;
}</pre>
</div>
<p>&nbsp;</p>
<h3>非变量</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">加</span>
    width: (10px+3<span style="color: #000000;">);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">减</span>
    height: (10px-4<span style="color: #000000;">);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">乘</span>
    margin: (8px*4<span style="color: #000000;">);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">除</span>
    border: (8px/2);
    <span style="color: #008000;">//</span><span style="color: #008000;">注：非变量的加减乘除要在()里面，几个数之间只需要一个带单位即可</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>颜色运算</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div{
   $color1:#fe0325;
   $color2:#c8f9l3;
   
   </span><span style="color: #008000;">//</span><span style="color: #008000;">两个16进制的数值相加（即将淘汰）</span>
   color: $color1 +<span style="color: #000000;"> $color2; 
   
   </span><span style="color: #008000;">//</span><span style="color: #008000;">两种颜色混合</span>
<span style="color: #000000;">   colour:mix($color1,$color2);

   
   color: red($color1);</span><span style="color: #008000;">//</span><span style="color: #008000;">获取$color1的红色素</span>
<span style="color: #000000;">   
   color: green($color1);</span><span style="color: #008000;">//</span><span style="color: #008000;">获取$color1的绿色素</span>
<span style="color: #000000;">   
   color: blue($color1);</span><span style="color: #008000;">//</span><span style="color: #008000;">获取$color1的蓝色素</span>
   
   <span style="color: #008000;">//</span><span style="color: #008000;">输出结果与$color1的值相同</span>
<span style="color: #000000;">   color: rgb(red($color1),green($color1),blue($color1));
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>字符串运算（介绍string类型时说过）</h3>
<div class="cnblogs_code">
<pre>$str:'asdff.png'<span style="color: #000000;">
.div{
    background</span>-image:url('../shanghai/'+<span style="color: #000000;">$str);
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>一般的mixin（混合宏）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">定义时：@mixin 名字 {}  ，里面可以放各种样式</span>
<span style="color: #000000;">@mixin hello{
    display: block;
    font: {
        size: 20px;<br />　　　　　weight:500;
    };
    color:blue;
}

.div{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">引入时：@include 名字</span>
<span style="color: #000000;">    @include hello;
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>嵌套的mixin</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">@mixin hello{
    display: block;
    font</span>-<span style="color: #000000;">size: 20px;;
    color:blue;
}
@mixin hi{
    name:hello;
    age:</span>18<span style="color: #000000;">;
    @include hello;  </span><span style="color: #008000;">//</span><span style="color: #008000;">这里尾部，引入hello代码块</span>
<span style="color: #000000;">}
.div{
    cursor: pointer;
    @include hi;    </span><span style="color: #008000;">//</span><span style="color: #008000;">这里引入hi代码块</span>
    font-family: "agency fb"<span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>带参数的mixin</h3>
<div class="cnblogs_code">
<pre>@mixin seeyou($name,$age){  <span style="color: #008000;">//</span><span style="color: #008000;">这里可以用,隔开，接收多个参数</span>
<span style="color: #000000;">    name:$name;
    age:$age;
    border: 88px;
}
.div{
    @include seeyou(</span>'zhangsan',18); <span style="color: #008000;">//</span><span style="color: #008000;">这里调用mixin的时候要给实参</span>
}</pre>
</div>
<p>&nbsp;</p>
<h2>Sass继承</h2>
<h3>简单继承</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div1{
    color: red;
}
.div2{
    @extend .div1;  </span><span style="color: #008000;">//</span><span style="color: #008000;">继承：@extend 需要继承选择器的名字</span>
    background-<span style="color: #000000;">color: blue;
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>关联属性继承&nbsp;</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div1{
    color: red;
}
.div1.other{
    background</span>-<span style="color: #000000;">color: blue;
}
.dd{
    @extend .div1; </span><span style="color: #008000;">//</span><span style="color: #008000;">不单单继承div1，选择器中包含div1的也继承</span>
}</pre>
</div>
<h3>&nbsp;</h3>
<h3>链式继承&nbsp;</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div1{
    color: red;
}
.div2{
    background</span>-<span style="color: #000000;">color: blue;
    @extend .div1;  </span><span style="color: #008000;">//</span><span style="color: #008000;">继承了div1</span>
<span style="color: #000000;">}
.dd{
    cursor: pointer;
    @extend .div2;  </span><span style="color: #008000;">//</span><span style="color: #008000;">不仅继承div2，div2里面继承了div1，所以div1跟div2都继承了</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>伪类继承</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">a:hover{
    background</span>-<span style="color: #000000;">color: red;
}
.div{
    @extend :hover; </span><span style="color: #008000;">//</span><span style="color: #008000;">继承了a的伪类</span>
<span style="color: #000000;">    color: black;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>Sass嵌套</h2>
<h3>一般嵌套.</h3>
<p>div &gt; .inner &gt; .cc</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div{
    color: cyan;
    font</span>-<span style="color: #000000;">size: 30px;
    .inner{    </span><span style="color: #008000;">//</span><span style="color: #008000;">div里面的inner</span>
<span style="color: #000000;">        position: relative;
        top: 20px;
        left: 10px;
        .cc{    </span><span style="color: #008000;">//</span><span style="color: #008000;">div里面的inner里面的cc</span>
<span style="color: #000000;">            width: 200px;
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>特殊嵌套</h3>
<p>一般以横杠分离的属性都可以嵌套，如：background-color、background-clip，可把color、clip嵌套到background里面去</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div{
    background:{
        image:url(</span>'../haha.jpg');   <span style="color: #008000;">//</span><span style="color: #008000;">表示background-image</span>
        clip: border-box;       <span style="color: #008000;">//</span><span style="color: #008000;">表示background-clip</span>
<span style="color: #000000;">    };
    font:{
        size: 30px;     </span><span style="color: #008000;">//</span><span style="color: #008000;">表示font-size</span>
        family:'abc';   <span style="color: #008000;">//</span><span style="color: #008000;">表示font-family</span>
<span style="color: #000000;">    };
}</span>&nbsp;</pre>
</div>
<p>&nbsp;</p>
<h2>Sass条件控制语句</h2>
<h3>if else 语句</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> {}里面可以用</span>
$name:'zhangsan'<span style="color: #000000;">;
.div{
    @</span><span style="color: #0000ff;">if</span> $name == 'lisi'<span style="color: #000000;">{
        color: red;
    }@</span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> $name == 'xiaoming'<span style="color: #000000;">{
        color: orange;
    }@</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
        color: purple;
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">注意if else 语句前面记得加@，判断语句不需要括号</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">{}外面也能使用</span>
@<span style="color: #0000ff;">if</span> $name == '123'<span style="color: #000000;">{
    .div{
        position: absolute;
    }
}@</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
    .bb{
        height: 30px;
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>for语句</h3>
<div class="cnblogs_code">
<pre>@<span style="color: #0000ff;">for</span> $i from 1 through 5{   <span style="color: #008000;">//</span><span style="color: #008000;">循环1-5次，包含第5次，实际5次</span>
<span style="color: #000000;">    .cc#{$i}{
        color: blue;
    }
}
@</span><span style="color: #0000ff;">for</span> $i from 1 to 5{    <span style="color: #008000;">//</span><span style="color: #008000;">循环1-5次，不包含第5次，实际4次</span>
<span style="color: #000000;">    .aa#{$i}{
        color: blue;
    }
}</span>&nbsp;</pre>
</div>
<p>&nbsp;</p>
<h3>for遍历list</h3>
<div class="cnblogs_code">
<pre>$list:(1,2,3,4,5<span style="color: #000000;">);
@</span><span style="color: #0000ff;">for</span> $i from 1 through length($list){    <span style="color: #008000;">//</span><span style="color: #008000;">遍历一般用through，length($list)表示$list的数组长度</span>
<span style="color: #000000;">    .div#{$i} {
        width: 100px;
    }
}</span></pre>
</div>
<p>&nbsp;&nbsp;</p>
<h3>while语句</h3>
<div class="cnblogs_code">
<pre>$i:1<span style="color: #000000;">;
@</span><span style="color: #0000ff;">while</span> $i&lt;5 {   <span style="color: #008000;">//</span><span style="color: #008000;">符合条件才能进入循环</span>
<span style="color: #000000;">    .div#{$i} {
        color: white;
    }
    $i:$i</span>+1;    <span style="color: #008000;">//</span><span style="color: #008000;">记得要对循环数做操作，不然报错死循环</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>each遍历map</h3>
<div class="cnblogs_code">
<pre>$map:(top:10px,right:10px,bottom:5px,left:7px); <span style="color: #008000;">//</span><span style="color: #008000;">记得map是用()的</span>
<span style="color: #000000;">.div{
    @each $key,$value </span><span style="color: #0000ff;">in</span> $map {     <span style="color: #008000;">//</span><span style="color: #008000;">$key表示键，$value表示值</span>
        #{$key}:$value;   <span style="color: #008000;">//</span><span style="color: #008000;">将键值对循环输出</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&nbsp;内置函数</h2>
<h3>Number函数</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">.div {
    zoom: percentage(</span>0.33); <span style="color: #008000;">//</span><span style="color: #008000;">转换为百分比</span>
<span style="color: #000000;">    
    zoom: round(</span>4.5);   <span style="color: #008000;">//</span><span style="color: #008000;">四舍五入</span>
<span style="color: #000000;">    
    zoom: ceil(</span>22.5);   <span style="color: #008000;">//</span><span style="color: #008000;">向上取整</span>
<span style="color: #000000;">    
    zoom: floor(</span>22.5);  <span style="color: #008000;">//</span><span style="color: #008000;">向下取整</span>
<span style="color: #000000;">    
    zoom: abs(</span>-33);    <span style="color: #008000;">//</span><span style="color: #008000;">取绝对值</span>
<span style="color: #000000;">    
    zoom: random(</span>10);   <span style="color: #008000;">//</span><span style="color: #008000;">取0-10之间的数，若省略数字，则取0-1之间的数</span>
<span style="color: #000000;">    
    $a: </span>1<span style="color: #000000;">;
    $b: </span>2<span style="color: #000000;">;
    $c: </span>3<span style="color: #000000;">;
    zoom: min($a, $b, $c);  </span><span style="color: #008000;">//</span><span style="color: #008000;">取最小值，里面必须是变量，切要两个以上</span>
    zoom: max($a, $b, $c);  <span style="color: #008000;">//</span><span style="color: #008000;">取最大值，规则同上</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>List函数（数组）&nbsp;</h3>
<div class="cnblogs_code">
<pre>$list:(5,4,3,2,1<span style="color: #000000;">);

@debug length($list);    </span><span style="color: #008000;">//</span><span style="color: #008000;">获取数组长度</span>
<span style="color: #000000;">
@debug nth($list,</span>3);    <span style="color: #008000;">//</span><span style="color: #008000;">获取指定数组下标的元素</span>
<span style="color: #000000;">
@debug set</span>-nth($list,1,'bb');    <span style="color: #008000;">//</span><span style="color: #008000;">获取下标为1的元素，替换为bb</span>
<span style="color: #000000;">
$list2:(</span>'aa','bb','cc'<span style="color: #000000;">);

@debug join($list,$list2);        </span><span style="color: #008000;">//</span><span style="color: #008000;">将$list和$list2拼接在一起。只能两个数组拼接</span>
@debug join($list,(33,44<span style="color: #000000;">));

@debug append($list2,</span>'dd');    <span style="color: #008000;">//</span><span style="color: #008000;">将'dd'拼接到数组后面</span>
<span style="color: #000000;">
@debug index($list2,</span>'ff');     <span style="color: #008000;">//</span><span style="color: #008000;">查找'aa'是否存在，存在返回下标，不存在返回null</span></pre>
</div>
<p>&nbsp;</p>
<h3>String函数（字符串）</h3>
<div class="cnblogs_code">
<pre>$da:'HELLO'<span style="color: #000000;">;
$xiao:hello;
.div{
    color:unquote($da);      </span><span style="color: #008000;">//</span><span style="color: #008000;">去除字符串引号</span>
    color:quote($xiao);      <span style="color: #008000;">//</span><span style="color: #008000;">添加字符串引号</span>
<span style="color: #000000;">    } 
@debug str</span>-length($xiao);     <span style="color: #008000;">//</span><span style="color: #008000;">获取字符串长度</span>
<span style="color: #000000;">
@debug str</span>-index($xiao,'c');    <span style="color: #008000;">//</span><span style="color: #008000;">查看字符串是否存在'e'，存在返回下标，不存在返回null</span>
<span style="color: #000000;">
@debug to</span>-upper-<span style="color: #0000ff;">case</span>($xiao);    <span style="color: #008000;">//</span><span style="color: #008000;">小写转大写</span>
@debug to-lower-<span style="color: #0000ff;">case</span>($da);        <span style="color: #008000;">//</span><span style="color: #008000;">大写转小写</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;Map函数（对象）</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">$map:(top:10px,right:10px,bottom:5px,left:7px);

@debug map</span>-get($map,top);    <span style="color: #008000;">//</span><span style="color: #008000;">获取$map的top，若存在返回所对应的value值，若不存在返回null</span>
@debug map-has-key($map,top);    <span style="color: #008000;">//</span><span style="color: #008000;">查看$map是否有top这个key值，有就返回true，否则false</span>
<span style="color: #000000;">
@debug map</span>-remove($map,top);    <span style="color: #008000;">//</span><span style="color: #008000;">删除$map里面的top值，后返回剩下的key和value</span>
<span style="color: #000000;">
@debug map</span>-keys($map);    <span style="color: #008000;">//</span><span style="color: #008000;">返回$map的所有key值</span>
@debug map-values($map);    <span style="color: #008000;">//</span><span style="color: #008000;">返回$map的所有value值</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">@mixin hello($ags...){
    @debug keywords($ags);    </span><span style="color: #008000;">//</span><span style="color: #008000;">用keywords方法，打印出接收到的所有参数</span>
<span style="color: #000000;">}
@include hello($name:</span>'zhangsan',$sex:'male',$age:18);    <span style="color: #008000;">//</span><span style="color: #008000;">注意：key值要以$开头</span></pre>
</div>
<p>&nbsp;</p>
<h3>Function函数</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">自定义函数</span>
@<span style="color: #0000ff;">function</span> haha($aa,$bb){  <span style="color: #008000;">//</span><span style="color: #008000;">接收两个参数</span>
    @<span style="color: #0000ff;">return</span> $aa+$bb;   <span style="color: #008000;">//</span><span style="color: #008000;">返回两个参数相加的结果</span>
<span style="color: #000000;">}
.div{
    width: haha(10px,20px);  </span><span style="color: #008000;">//</span><span style="color: #008000;">调用haha函数，并按照需求传入两个参数</span>
}</pre>
</div>
<p>&nbsp;</p>
