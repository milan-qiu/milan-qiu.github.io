---
title: "10、Controller之Middleware"
date: "2020-06-22 22:17:00"
updated: "2020-07-01 19:46:00"
tags:
categories:
description: >-
  路由中间件：达到某些要求就可以访问这个页面，达不到要求访问那个页面 一、编写控制器 public function middle1(){ return '尚未达到要求'; } public function middle2(){ return '已达到要求，访问中'; } 二、新建中间件，在 app
---

<p>路由中间件：达到某些要求就可以访问这个页面，达不到要求访问那个页面</p>
<p>&nbsp;</p>
<p>一、编写控制器</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function middle1(){
    </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">'</span><span style="color: #800000;">尚未达到要求</span><span style="color: #800000;">'</span><span style="color: #000000;">;
}
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function middle2(){
    </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">'</span><span style="color: #800000;">已达到要求，访问中</span><span style="color: #800000;">'</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>二、新建中间件，在 app / Http / Middleware 下，新建 Huodong.php</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php
</span><span style="color: #0000ff;">namespace</span> App\Http\Middleware; <span style="color: #008000;">//</span><span style="color: #008000;">命名空间</span>
<span style="color: #000000;">use Closure;

</span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Huodong{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function handle($request,Closure $next){ 
        </span><span style="color: #008000;">//</span><span style="color: #008000;">写要求</span>
        <span style="color: #0000ff;">if</span>(time() &lt; strtotime(<span style="color: #800000;">'</span><span style="color: #800000;">2020-6-26</span><span style="color: #800000;">'</span><span style="color: #000000;">)){
            </span><span style="color: #0000ff;">return</span> redirect(<span style="color: #800000;">'</span><span style="color: #800000;">middle1</span><span style="color: #800000;">'</span><span style="color: #000000;">);
        }
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> $next($request);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>三、注册中间件，app / Http / Kernel.php ，路由中间件在&nbsp; protected $routeMiddleware 里面添加</p>
<div class="cnblogs_code">
<pre><span style="color: #800000;">'</span><span style="color: #800000;">huodong</span><span style="color: #800000;">'</span> =&gt; \App\Http\Middleware\Huodong::<span style="color: #0000ff;">class</span><span style="color: #000000;">,
</span><span style="color: #008000;">//</span><span style="color: #008000;">中间件名字  ，中间件页面位置 ::class</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>四、编写路由</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">不需要条件，可做宣传页</span>
Route::<span style="color: #0000ff;">get</span>(<span style="color: #800000;">'</span><span style="color: #800000;">/middle1</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">XxxController@middle1</span><span style="color: #800000;">'</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">条件到达可访问，可做活动页，里面可以设置多个路由</span>
Route::group([<span style="color: #800000;">'</span><span style="color: #800000;">middleware</span><span style="color: #800000;">'</span> =&gt; [<span style="color: #800000;">'</span><span style="color: #800000;">huodong</span><span style="color: #800000;">'</span><span style="color: #000000;">]],function(){
                         </span><span style="color: #008000;">//</span><span style="color: #008000;">注册中间件时的名字</span>
<span style="color: #000000;">
    Route::</span><span style="color: #0000ff;">get</span>(<span style="color: #800000;">'</span><span style="color: #800000;">/middle2</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">XxxController@middle2</span><span style="color: #800000;">'</span><span style="color: #000000;">);
});</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>辨别 前置 / 后置 中间件，在写中间件页面时判断&nbsp;$next($request) 的先后顺序</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php
</span><span style="color: #0000ff;">namespace</span> App\Http\Middleware; <span style="color: #008000;">//</span><span style="color: #008000;">命名空间</span>
<span style="color: #000000;">use Closure;

</span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Huodong{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function handle($request,Closure $next){ 

        </span><span style="color: #0000ff;">if</span>(time() &lt; strtotime(<span style="color: #800000;">'</span><span style="color: #800000;">2020-6-26</span><span style="color: #800000;">'</span><span style="color: #000000;">)){
            </span><span style="color: #0000ff;">return</span> redirect(<span style="color: #800000;">'</span><span style="color: #800000;">middle1</span><span style="color: #800000;">'</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">return</span> $next($request); <span style="color: #008000;">//</span><span style="color: #008000;">这是前置中间件
        </span><span style="color: #008000;">//</span><span style="color: #008000;">在这个请求之前操作，前置中间件
        </span><span style="color: #008000;">//</span><span style="color: #008000;">在这个请求之后操作，后置中间件</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
