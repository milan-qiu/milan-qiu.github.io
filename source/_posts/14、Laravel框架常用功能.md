---
title: "14、Laravel框架常用功能"
date: "2020-07-03 23:10:00"
updated: "2020-07-04 01:23:00"
tags:
categories:
description: >-
  文件上传 配置文件 config -> filesystems.php，可以使用原有的磁盘，也可以新建磁盘 一、新建磁盘 'upload' => [ 'driver' => 'local', 'root' => storage_path('app/public'), //上传目录为 storage/
---

<h2>文件上传</h2>
<p>配置文件 config -&gt; filesystems.php，可以使用原有的磁盘，也可以新建磁盘</p>
<p>一、新建磁盘</p>
<div class="cnblogs_code">
<pre><span style="color: #800000;">'</span><span style="color: #800000;">upload</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> [
    </span><span style="color: #800000;">'</span><span style="color: #800000;">driver</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">local</span><span style="color: #800000;">'</span><span style="color: #000000;">,
    </span><span style="color: #800000;">'</span><span style="color: #800000;">root</span><span style="color: #800000;">'</span> =&gt; storage_path(<span style="color: #800000;">'</span><span style="color: #800000;">app/public</span><span style="color: #800000;">'</span><span style="color: #000000;">),  //上传目录为 storage/app/public/<br />  //'root' =&gt; public_path('upload'),  //上传目录为 public/upload/ 
],</span></pre>
</div>
<p>&nbsp;</p>
<p>二、配置路由，配置控制器</p>
<p>1、控制器引入Storage</p>
<div class="cnblogs_code">
<pre>use Illuminate\Support\Facades\Storage;</pre>
</div>
<p>&nbsp;</p>
<p>2、控制器引入Request</p>
<div class="cnblogs_code">
<pre>use Illuminate\Http\Request;</pre>
</div>
<p>&nbsp;</p>
<p>3、新建方法</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function upload(Request $request){
    </span><span style="color: #0000ff;">if</span>($request-&gt;isMethod(<span style="color: #800000;">'</span><span style="color: #800000;">POST</span><span style="color: #800000;">'</span><span style="color: #000000;">)){
        $file </span>= $request-&gt;file(<span style="color: #800000;">'</span><span style="color: #800000;">source</span><span style="color: #800000;">'</span><span style="color: #000000;">);
        </span><span style="color: #008000;">//</span><span style="color: #008000;">文件是否上传成功</span>
        <span style="color: #0000ff;">if</span>($file-&gt;<span style="color: #000000;">isValid()){
            </span><span style="color: #008000;">//</span><span style="color: #008000;">原文件名</span>
            $originalName = $file-&gt;<span style="color: #000000;">getClientOriginalName();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">扩展名</span>
            $ext = $file-&gt;<span style="color: #000000;">getClientOriginalExtension();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">文件类型</span>
            $type = $file-&gt;<span style="color: #000000;">getClientMimeType();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">临时绝对路径</span>
            $realPath = $file-&gt;<span style="color: #000000;">getRealPath();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">上传后的文件名</span>
            $filename = date(<span style="color: #800000;">'</span><span style="color: #800000;">Y-m-d-H-i-s</span><span style="color: #800000;">'</span>) . <span style="color: #800000;">'</span><span style="color: #800000;">-</span><span style="color: #800000;">'</span> . uniqid() . <span style="color: #800000;">'</span><span style="color: #800000;">.</span><span style="color: #800000;">'</span><span style="color: #000000;"> . $ext;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">执行上传</span>
            $<span style="color: #0000ff;">bool</span> = Storage::disk(<span style="color: #800000;">'</span><span style="color: #800000;">upload</span><span style="color: #800000;">'</span>)-&gt;<span style="color: #000000;">put($filename,file_get_contents($realPath)); //第一个参数文件名，第二个参数为源文件临时路径
            var_dump($</span><span style="color: #0000ff;">bool</span><span style="color: #000000;">); //上传成功返回true
        }
        exit;
    }
    </span><span style="color: #0000ff;">return</span> view(<span style="color: #800000;">'</span><span style="color: #800000;">Xxx.upload</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>4、新建视图</p>
<div class="cnblogs_code">
<pre>&lt;form action=<span style="color: #800000;">""</span> method=<span style="color: #800000;">"</span><span style="color: #800000;">POST</span><span style="color: #800000;">"</span> enctype=<span style="color: #800000;">"</span><span style="color: #800000;">multipart/form-data</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
    @csrf
    </span>&lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">file</span><span style="color: #800000;">"</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">file</span><span style="color: #800000;">"</span> name=<span style="color: #800000;">"</span><span style="color: #800000;">source</span><span style="color: #800000;">"</span>/&gt;
    &lt;button type=<span style="color: #800000;">"</span><span style="color: #800000;">submit</span><span style="color: #800000;">"</span>&gt;上传&lt;/button&gt;
&lt;/form&gt;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>邮件发送</h2>
<p>配置文件 config / mail.php，</p>
<p>default里面配置默认驱动，smtp（16行左右）</p>
<p>from里面配置发件人邮箱、名称（84行左右）</p>
<p>mailers -&gt; smtp -&gt; host、port、encryption&nbsp; 配置发送邮件的主机地址、端口、协议（具体信息在.env里面填写）</p>
<p>&nbsp;</p>
<h2>缓存的使用</h2>
<p>一、控制器引入</p>
<div class="cnblogs_code">
<pre>use Illuminate\Support\Facades\Cache;</pre>
</div>
<p>&nbsp;</p>
<p>二、各种方法使用</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function cache1(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">put添加键值对，设置时长，单位秒</span>
    Cache::put(<span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span>,<span style="color: #800000;">'</span><span style="color: #800000;">val1</span><span style="color: #800000;">'</span>,<span style="color: #800080;">60</span><span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">add判断是否存在该键，存在就不添加并返回false，不存在就添加并返回true
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> $bool = Cache::add('key2','val2',20);
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var_dump($bool);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">forever永久保存该键值对
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Cache::forever('key3','val3');

    </span><span style="color: #008000;">//</span><span style="color: #008000;">has判断该键是否存在
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> if(Cache::has('key3')){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">     echo 'key3存在';
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> }</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> function cache2(){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">get获取缓存的值
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> $key1 = Cache::get('key1');
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var_dump($key1);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">pull取出键值对后立即删除
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> $val = Cache::pull('key3');
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var_dump($val);

    </span><span style="color: #008000;">//</span><span style="color: #008000;">forget删除某个键，返回布尔值</span>
    $<span style="color: #0000ff;">bool</span> = Cache::forget(<span style="color: #800000;">'</span><span style="color: #800000;">key1</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    var_dump($</span><span style="color: #0000ff;">bool</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>错误与日志</h2>
<h3>Debug模式</h3>
<p>一、配置文件：config / app.php&nbsp;</p>
<p>二、默认在.env文件里面填入true/false（.env第4行）</p>
<p>三、代码上线后debug模式要设置为false</p>
<p>&nbsp;</p>
<h3>HTTP异常</h3>
<p>一、判断到http异常就抛出状态码</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function error(){
    $stt </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span>($stt==<span style="color: #0000ff;">null</span><span style="color: #000000;">){
        abort(</span><span style="color: #800000;">'</span><span style="color: #800000;">500</span><span style="color: #800000;">'</span>); <span style="color: #008000;">//</span><span style="color: #008000;">除了500还有其他的，如404等等</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>日志</h3>
<p>配置文件在 config -&gt; logging.php ，默认选择stack日志驱动。更改需要在.env文件的第七行进行。</p>
<p>Laravel日志支持&nbsp;single、daily、slack、syslog、errorlog、monolog、custom、stack 等日志驱动</p>
<p>官方文档：<a href="https://learnku.com/docs/laravel/7.x/logging/7469">https://learnku.com/docs/laravel/7.x/logging/7469</a></p>
<p><strong>single驱动</strong></p>
<p>一、生成的日志文件在 storage / logs 下的 laravel.log</p>
<p>二、控制器引入</p>
<div class="cnblogs_code">
<pre>use Illuminate\Support\Facades\Log;</pre>
</div>
<p>&nbsp;</p>
<p>三、控制器发生错误时，将错误写进日志</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function error(){
    $stt </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span>($stt==<span style="color: #0000ff;">null</span><span style="color: #000000;">){
        Log::info(</span><span style="color: #800000;">'</span><span style="color: #800000;">这是info级别的日志</span><span style="color: #800000;">'</span><span style="color: #000000;">);
        abort(</span><span style="color: #800000;">'</span><span style="color: #800000;">500</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">除了info级别的还有，debug、notice、warning、error、critical、alert 级别的日志。</span></pre>
</div>
<p>&nbsp;</p>
<h2>队列</h2>
<p>作用：允许推迟耗时任务（如发送邮件）的执行，从而大幅度提升web请求速度。</p>
<p>配置文件：config / queue.php 。默认为同步驱动sync，在.env里面更改(18行左右)。</p>
<p>支持的驱动有：sync、database、beanstalkd、sqs、redis、null</p>
<h3>Database驱动</h3>
<p><strong>一、迁移队列需要的数据表</strong>（生成的job表和fail_job表，在database/migrations里面）</p>
<div class="cnblogs_code">
<pre> php artisan queue:table</pre>
</div>
<p>&nbsp;</p>
<p>执行迁移</p>
<div class="cnblogs_code">
<pre>php artisan migrate</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>二、编写任务类</strong>（生成的文件在Jobs / SeedMail.php）</p>
<div class="cnblogs_code">
<pre>php artisan make:job SeedMail</pre>
</div>
<p>&nbsp;</p>
<p>编写SeedMail.php</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> App\Jobs;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Foundation\Bus\Dispatchable;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Queue\SerializesModels;
use Mail;<br />use Illuminate\Support\Facades\Log;

</span><span style="color: #0000ff;">class</span><span style="color: #000000;"> SeedMail implements ShouldQueue
{
    use Dispatchable, InteractsWithQueue, Queueable, SerializesModels;
    </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> $email;
</span>
    <span style="color: #0000ff;">public</span><span style="color: #000000;"> function __construct($email)
    {
        </span><span style="color: #008000;">//接收参数
</span>        $<span style="color: #0000ff;">this</span> -&gt; email =<span style="color: #000000;"> $email;
    }
</span>
    <span style="color: #0000ff;">public</span><span style="color: #000000;"> function handle()
    {
        </span><span style="color: #008000;">//队列任务
</span>        //Mail::raw(<span style="color: #800000;">'</span><span style="color: #800000;">队列测h</span><span style="color: #800000;">'</span><span style="color: #000000;">,function($message){
            //$message</span>-&gt;to($<span style="color: #0000ff;">this</span>-&gt;<span style="color: #000000;">email);
        //});<br />        Log::info('模拟发送邮件-&gt;' . $this-&gt;email);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>三、推送任务到队列</strong></p>
<p>控制器引入</p>
<div class="cnblogs_code">
<pre>use DispatchesJobs; <span style="color: #008000;">//</span><span style="color: #008000;">使用DispatchesJobs</span>
use App\Jobs\SeedMail; <span style="color: #008000;">//</span><span style="color: #008000;">使用队列</span></pre>
</div>
<p>&nbsp;</p>
<p>编写方法</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> function queue(){
    dispatch(</span><span style="color: #0000ff;">new</span> SeedMail(<span style="color: #800000;">'</span><span style="color: #800000;">83962159@qq.com</span><span style="color: #800000;">'</span><span style="color: #000000;">));
}</span></pre>
</div>
<p>&nbsp;</p>
<p>运行方法，此时jobs表就有数据了（报错？）</p>
<p>&nbsp;</p>
<p><strong>四、运行队列监听器</strong></p>
<div class="cnblogs_code">
<pre>php artisan queue:listen</pre>
</div>
<p>&nbsp;</p>
<p>这时便执行队列中的任务（如邮件发送）</p>
<p>&nbsp;</p>
<p><strong>五、处理失败任务</strong></p>
<p>查看失败记录</p>
<div class="cnblogs_code">
<pre>php artisan queue:failed</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>重新执行某条任务（id为1的那条）</p>
<div class="cnblogs_code">
<pre>php artisan queue:retry <span style="color: #800080;">1</span></pre>
</div>
<p>&nbsp;</p>
<p>重新执行失败记录里的所有任务</p>
<div class="cnblogs_code">
<pre>php artisan queue:retry all</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>删除某条失败记录的任务（id为2的）</p>
<div class="cnblogs_code">
<pre>php artisan queue:forget <span style="color: #800080;">2</span></pre>
</div>
<p>&nbsp;</p>
<p>删除某条失败记录的所有任务</p>
<div class="cnblogs_code">
<pre>php artisan queue:flush</pre>
</div>
<p>&nbsp;</p>
