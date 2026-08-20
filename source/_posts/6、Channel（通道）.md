---
title: "6、Channel（通道）"
date: "2022-02-27 13:44:00"
updated: "2022-03-01 18:00:00"
tags:
categories:
description: >-
  简单收发channel func main() { chanDemo() } func chanDemo() { c := make(chan int) go func() { for { n := <- c // 接收 channel 的数据 fmt.Println(n) } }() // 发送
---

<h2>简单收发channel</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main()  {
    chanDemo()
}

func chanDemo() {
    c :</span>= make(chan <span style="color: #0000ff;">int</span><span style="color: #000000;">)
    go func() {
        </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> {
            n :</span>= &lt;- c <span style="color: #008000;">//</span><span style="color: #008000;"> 接收 channel 的数据</span>
<span style="color: #000000;">            fmt.Println(n)
        }
    }()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 发送 channel 数据</span>
    c &lt;- <span style="color: #800080;">1</span><span style="color: #000000;">
    c </span>&lt;- <span style="color: #800080;">2</span><span style="color: #000000;">

    time.Sleep(time.Millisecond)
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>channel 批量收发数据</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main()  {
    chanDemo()
}

func chanDemo() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义 channel 数组</span>
    <span style="color: #0000ff;">var</span> channels [<span style="color: #800080;">10</span>]chan <span style="color: #0000ff;">int</span>

    <span style="color: #008000;">//</span><span style="color: #008000;"> 批量收数据</span>
    <span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
        channels[i] </span>= make(chan <span style="color: #0000ff;">int</span><span style="color: #000000;">)
        go worker(i,channels[i])
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 批量发数据</span>
    <span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
        channels[i] </span>&lt;- i + <span style="color: #800000;">'</span><span style="color: #800000;">a</span><span style="color: #800000;">'</span><span style="color: #000000;">
    }

    time.Sleep(time.Millisecond)
}

func worker (i </span><span style="color: #0000ff;">int</span>, c chan <span style="color: #0000ff;">int</span><span style="color: #000000;">){
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> {
        n :</span>= &lt;- c <span style="color: #008000;">//</span><span style="color: #008000;"> 接收 channel 的数据</span>
        fmt.Printf(<span style="color: #800000;">"</span><span style="color: #800000;">接收来自 %d 通道，数据%v\n</span><span style="color: #800000;">"</span><span style="color: #000000;">,i,n)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>channel 通道类型</h2>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 双向通道</span>
<span style="color: #0000ff;">var</span> a chan <span style="color: #0000ff;">int</span>

<span style="color: #008000;">//</span><span style="color: #008000;"> 仅发送类型</span>
<span style="color: #0000ff;">var</span> b chan&lt;- <span style="color: #0000ff;">int</span>

<span style="color: #008000;">//</span><span style="color: #008000;">仅接收类型</span>
<span style="color: #0000ff;">var</span> c &lt;-chan <span style="color: #0000ff;">int</span></pre>
</div>
<p>&nbsp;</p>
<h2>channel 的缓冲区</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main()  {
    bufferedChan()
}

func bufferedChan() {
    c :</span>= make(chan <span style="color: #0000ff;">int</span>,<span style="color: #800080;">3</span>) <span style="color: #008000;">//</span><span style="color: #008000;"> 给通道设定缓冲区</span>
    go worker(<span style="color: #800080;">0</span><span style="color: #000000;">,c)
    c </span>&lt;- <span style="color: #800080;">11</span><span style="color: #000000;">
    c </span>&lt;- <span style="color: #800080;">22</span><span style="color: #000000;">
    c </span>&lt;- <span style="color: #800080;">33</span><span style="color: #000000;">
    close(c) </span><span style="color: #008000;">//</span><span style="color: #008000;"> 关闭通道</span>
<span style="color: #000000;">
    time.Sleep(time.Millisecond)
}

func worker (i </span><span style="color: #0000ff;">int</span>, c chan <span style="color: #0000ff;">int</span><span style="color: #000000;">){
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 若从通道收不到数据就退出
    </span><span style="color: #008000;">//</span><span style="color: #008000;">for {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    n,ok := &lt;- c
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    if !ok {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">        break
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">    fmt.Printf("接收来自 %d 通道，数据%v\n",i,n)
    </span><span style="color: #008000;">//</span><span style="color: #008000;">}

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 同理，若通道有数据就打印</span>
    <span style="color: #0000ff;">for</span> n :=<span style="color: #000000;"> range c {
        fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">接收来自 %d 通道，数据%v\n</span><span style="color: #800000;">"</span><span style="color: #000000;">,i,n)
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>channel 等待所有 goroutine 结束</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main()  {
    chanDemo()
}

type workStruct </span><span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    </span><span style="color: #0000ff;">in</span> chan <span style="color: #0000ff;">int</span><span style="color: #000000;">
    done chan </span><span style="color: #0000ff;">bool</span><span style="color: #000000;">
}

func chanDemo() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义 channel 数组</span>
    <span style="color: #0000ff;">var</span> channels [<span style="color: #800080;">10</span><span style="color: #000000;">]workStruct
    </span><span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
        channels[i] </span>=<span style="color: #000000;"> workStruct{
            </span><span style="color: #0000ff;">in</span> : make(chan <span style="color: #0000ff;">int</span><span style="color: #000000;">),
            done: make(chan </span><span style="color: #0000ff;">bool</span><span style="color: #000000;">),
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 批量收数据</span>
    <span style="color: #0000ff;">for</span> i,w :=<span style="color: #000000;"> range channels{</span>
<span style="color: #000000;">        go worker(i,w)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 批量发数据</span>
    <span style="color: #0000ff;">for</span> i,w :=<span style="color: #000000;"> range channels{
        w.</span><span style="color: #0000ff;">in</span> &lt;- <span style="color: #800000;">'</span><span style="color: #800000;">a</span><span style="color: #800000;">'</span> +<span style="color: #000000;"> i
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 当接收完 channels 里面的 done ，表示 channel 执行完毕</span>
    <span style="color: #0000ff;">for</span> _,w :=<span style="color: #000000;"> range channels{
        </span>&lt;-<span style="color: #000000;">w.done
        close(w.</span><span style="color: #0000ff;">in</span><span style="color: #000000;">)
        close(w.done)
    }

    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">执行后续操作</span><span style="color: #800000;">"</span><span style="color: #000000;">)
}

func worker (i </span><span style="color: #0000ff;">int</span><span style="color: #000000;">, c workStruct){
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 同理，若通道有数据就打印</span>
    <span style="color: #0000ff;">for</span> n := range c.<span style="color: #0000ff;">in</span><span style="color: #000000;"> {
        fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">接收来自 %d 通道，数据%v\n</span><span style="color: #800000;">"</span><span style="color: #000000;">,i,n)
        c.done </span>&lt;- <span style="color: #0000ff;">true</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<h2>&nbsp;</h2>
<h2>WaitGroup 等待所有 goroutine 结束</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main()  {
    chanDemo()
}

type workStruct </span><span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    </span><span style="color: #0000ff;">in</span> chan <span style="color: #0000ff;">int</span><span style="color: #000000;">
    wg </span>*<span style="color: #000000;">sync.WaitGroup
}

func chanDemo() {
    </span><span style="color: #0000ff;">var</span><span style="color: #000000;"> wg sync.WaitGroup

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义 channel 数组</span>
    <span style="color: #0000ff;">var</span> channels [<span style="color: #800080;">10</span><span style="color: #000000;">]workStruct
    </span><span style="color: #0000ff;">for</span> i := <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;"> {
        channels[i] </span>=<span style="color: #000000;"> workStruct{
            </span><span style="color: #0000ff;">in</span> : make(chan <span style="color: #0000ff;">int</span><span style="color: #000000;">),
            wg: </span>&amp;<span style="color: #000000;">wg,
        }
    }

    wg.Add(</span><span style="color: #800080;">10</span><span style="color: #000000;">)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 批量收数据</span>
    <span style="color: #0000ff;">for</span> i,w :=<span style="color: #000000;"> range channels{
        go worker(i,w)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 批量发数据</span>
    <span style="color: #0000ff;">for</span> i,w :=<span style="color: #000000;"> range channels{
        w.</span><span style="color: #0000ff;">in</span> &lt;- <span style="color: #800000;">'</span><span style="color: #800000;">a</span><span style="color: #800000;">'</span> +<span style="color: #000000;"> i
    }

    wg.Wait()

    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">执行后续操作</span><span style="color: #800000;">"</span><span style="color: #000000;">)
}

func worker (i </span><span style="color: #0000ff;">int</span><span style="color: #000000;">, c workStruct){
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 若通道有数据就打印</span>
    <span style="color: #0000ff;">for</span> n := range c.<span style="color: #0000ff;">in</span><span style="color: #000000;"> {
        fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">接收来自 %d 通道，数据%v\n</span><span style="color: #800000;">"</span><span style="color: #000000;">,i,n)
        c.wg.Done()
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>select 接收或发送某个 channel 的值</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    </span><span style="color: #0000ff;">var</span> c1, c2 =<span style="color: #000000;"> generator(), generator()
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> {
        </span><span style="color: #0000ff;">select</span><span style="color: #000000;"> {
        </span><span style="color: #0000ff;">case</span> n := &lt;-<span style="color: #000000;">c1:
            fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">c1里面来了数据</span><span style="color: #800000;">"</span><span style="color: #000000;">, n)
        </span><span style="color: #0000ff;">case</span> n := &lt;-<span style="color: #000000;">c1:    
            fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">走这里</span><span style="color: #800000;">"</span>, n) 
        <span style="color: #0000ff;">case</span> n := &lt;-<span style="color: #000000;">c2:
            fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">c2里面来了数据</span><span style="color: #800000;">"</span><span style="color: #000000;">, n)
        }
    }
}

func generator() chan </span><span style="color: #0000ff;">int</span><span style="color: #000000;"> {
    </span><span style="color: #0000ff;">out</span> := make(chan <span style="color: #0000ff;">int</span><span style="color: #000000;">)
    go func() {
        i :</span>= <span style="color: #800080;">0</span>
        <span style="color: #0000ff;">for</span><span style="color: #000000;"> {
            time.Sleep(time.Duration(rand.Intn(</span><span style="color: #800080;">100</span>)) *<span style="color: #000000;"> time.Millisecond)
            </span><span style="color: #0000ff;">out</span> &lt;-<span style="color: #000000;"> i
            i</span>++<span style="color: #000000;">
        }
    }()
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">out</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>以下描述了 select 语句的语法：</p>
<ul>
<ul>
<li>每个 case 都必须是一个通信</li>
<li>所有 channel 表达式都会被求值</li>
<li>所有被发送的表达式都会被求值</li>
<li>如果任意某个通信可以进行，它就执行，其他被忽略。</li>
<li>如果有多个 case 都可以运行，Select 会随机公平地选出一个执行。其他不会执行。<br />否则：<ol>
<li>如果有 default 子句，则执行该语句。</li>
<li>如果没有 default 子句，select 将阻塞，直到某个通信可以运行；Go 不会重新对 channel 或值进行求值。</li>

</ol></li>

</ul>
</ul>
<p>&nbsp;</p>
<h2>传统同步机制</h2>
<p>WaitGroup</p>
<p>Cond</p>
<p>Mutex</p>
<div class="cnblogs_code">
<pre>type atomicInt <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    value </span><span style="color: #0000ff;">int</span>
    <span style="color: #0000ff;">lock</span><span style="color: #000000;"> sync.Mutex
}

func (a </span>*<span style="color: #000000;">atomicInt) increment() {
    a.</span><span style="color: #0000ff;">lock</span><span style="color: #000000;">.Lock()
    defer a.</span><span style="color: #0000ff;">lock</span><span style="color: #000000;">.Unlock()
    a.value</span>++<span style="color: #000000;">
}

func (a </span>*atomicInt) <span style="color: #0000ff;">get</span>() <span style="color: #0000ff;">int</span><span style="color: #000000;"> {
    a.</span><span style="color: #0000ff;">lock</span><span style="color: #000000;">.Lock()
    defer a.</span><span style="color: #0000ff;">lock</span><span style="color: #000000;">.Unlock()
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">int</span><span style="color: #000000;">(a.value)
}

func main() {
    </span><span style="color: #0000ff;">var</span><span style="color: #000000;"> a atomicInt
    a.increment()
    go func() {
        a.increment()
    }()
    time.Sleep(time.Millisecond)
    fmt.Println(a.</span><span style="color: #0000ff;">get</span><span style="color: #000000;">())
}</span></pre>
</div>
<p>&nbsp;</p>
