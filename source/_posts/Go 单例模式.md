---
title: "Go 单例模式"
date: "2022-03-01 11:54:00"
tags:
categories:
description: >-
  为什么需要使用单例模式 type WebConfig struct { Port int } func GetConfig() *WebConfig { return &WebConfig{Port: 8080} } func main() { a := GetConfig() b := GetCo
---

<p>为什么需要使用单例模式</p>
<div class="cnblogs_code">
<pre>type WebConfig <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    Port </span><span style="color: #0000ff;">int</span><span style="color: #000000;">
}

func GetConfig() </span>*<span style="color: #000000;">WebConfig {
    </span><span style="color: #0000ff;">return</span> &amp;WebConfig{Port: <span style="color: #800080;">8080</span><span style="color: #000000;">}
}

func main() {
    a :</span>=<span style="color: #000000;"> GetConfig()
    b :</span>=<span style="color: #000000;"> GetConfig()
    c :</span>=<span style="color: #000000;"> GetConfig()
    fmt.Println(a,b,c) // 明明是一样的配置，却开了 3 个地址存储
}</span></pre>
</div>
<p>&nbsp;</p>
<p>实现单例模式，方法一（单协程可用，多协程会导致并发不安全）</p>
<div class="cnblogs_code">
<pre>type WebConfig <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    Port </span><span style="color: #0000ff;">int</span><span style="color: #000000;">
}

</span><span style="color: #0000ff;">var</span> aConfig *<span style="color: #000000;">WebConfig

func GetConfig() </span>*<span style="color: #000000;">WebConfig {
    </span><span style="color: #0000ff;">if</span> aConfig != nil { <span style="color: #008000;">//</span><span style="color: #008000;"> 这样就保证了config统一性，还减少了内存的占用</span>
        <span style="color: #0000ff;">return</span><span style="color: #000000;"> aConfig
    }
    </span><span style="color: #0000ff;">return</span> &amp;WebConfig{Port: <span style="color: #800080;">8080</span><span style="color: #000000;">}
}

func main() {
    a :</span>=<span style="color: #000000;"> GetConfig()
    b :</span>=<span style="color: #000000;"> GetConfig()
    c :</span>=<span style="color: #000000;"> GetConfig()
    fmt.Println(a,b,c)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>方法二（在方法一的基础上加锁）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span><span style="color: #000000;"> m sync.Mutex

func GetConfig() </span>*<span style="color: #000000;">WebConfig {
    m.Lock()
    defer m.Unlock()
    </span><span style="color: #0000ff;">if</span> aConfig != nil { <span style="color: #008000;">//</span><span style="color: #008000;"> 这样就保证了config统一性，还减少了内存的占用</span>
        <span style="color: #0000ff;">return</span><span style="color: #000000;"> aConfig
    }
    </span><span style="color: #0000ff;">return</span> &amp;WebConfig{Port: <span style="color: #800080;">8080</span><span style="color: #000000;">}
}</span></pre>
</div>
<p>&nbsp;</p>
<p>方法三，使用Once（性能最高）</p>
<div class="cnblogs_code">
<pre>type WebConfig <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    Port </span><span style="color: #0000ff;">int</span><span style="color: #000000;">
}

</span><span style="color: #0000ff;">var</span> aConfig *<span style="color: #000000;">WebConfig

</span><span style="color: #0000ff;">var</span><span style="color: #000000;"> once sync.Once

func GetConfig() </span>*<span style="color: #000000;">WebConfig {
    once.Do(func() {
        aConfig </span>= &amp;WebConfig{Port: <span style="color: #800080;">8080</span><span style="color: #000000;">}
    })
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> aConfig
}

func main() {
    a :</span>=<span style="color: #000000;"> GetConfig()
    b :</span>=<span style="color: #000000;"> GetConfig()
    c :</span>=<span style="color: #000000;"> GetConfig()
    fmt.Println(a,b,c)
}</span></pre>
</div>
<p>&nbsp;</p>
