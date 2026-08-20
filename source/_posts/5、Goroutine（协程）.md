---
title: "5、Goroutine（协程）"
date: "2022-02-27 08:10:00"
tags:
categories:
description: >-
  routine 协程 轻量级“线程” 非抢占式多任务处理，由协程主动交出控制权 编译器 / 解释器 / 虚拟机层面的多任务 多个协程可能在一个或多个线程上运行（线程数量一般不大于机器核数） goroutine 并发栗子 func main() { for i := 0; i < 1000; i++
---

<h2>routine 协程</h2>
<p><span style="font-size: 14px;">轻量级&ldquo;线程&rdquo;</span></p>
<p>非抢占式多任务处理，由协程主动交出控制权</p>
<p>编译器 / 解释器 / 虚拟机层面的多任务</p>
<p>多个协程可能在一个或多个线程上运行（线程数量一般不大于机器核数）</p>
<p>&nbsp;</p>
<h2>goroutine 并发栗子</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main()  {
    </span><span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">1000</span>; i++<span style="color: #000000;"> {
        go func(j </span><span style="color: #0000ff;">int</span><span style="color: #000000;">) {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">for {</span>
                fmt.Println(<span style="color: #800000;">"</span><span style="color: #800000;">i am routine</span><span style="color: #800000;">"</span><span style="color: #000000;">,j)<br />　　　　　　　　　　// runtime.Gosched() // 手动交出控制权
            </span><span style="color: #008000;">//</span><span style="color: #008000;">}</span>
<span style="color: #000000;">        }(i)
    }
    time.Sleep(time.Millisecond)
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>goroutine 可能会切换的点</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">解释：
任何函数加上go就能送到调度器运行
调度器会在合适的位置进行协程的切换</span></pre>
</div>
<p>I/O,select</p>
<p>channel</p>
<p>等待锁</p>
<p>函数调用（有时）</p>
<p>runtime.Gosched()</p>
<p>&nbsp;</p>
<h2>检测数据访问冲突（检测race condition）</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main()  {
    a :</span>= <span style="color: #800080;">1</span>
    <span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">1000</span>; i++<span style="color: #000000;"> {
        go func(j </span><span style="color: #0000ff;">int</span>) { <span style="color: #008000;">//</span><span style="color: #008000;">race condition</span>
            <span style="color: #0000ff;">for</span><span style="color: #000000;"> {
                a</span>++<span style="color: #000000;">
            }
        }(i)
    }
    time.Sleep(time.Millisecond)
}</span></pre>
</div>
<p>检测命令</p>
<div class="cnblogs_code">
<pre>go run -race test.go</pre>
</div>
<p>&nbsp;</p>
