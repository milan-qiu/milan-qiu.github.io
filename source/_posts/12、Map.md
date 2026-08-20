---
title: "12、Map"
date: "2021-11-20 16:28:00"
tags:
categories:
description: >-
  package main import "fmt" func main() { // map // 直接定义 map m := map[string]int { "age":18, "name":11, "otherName":12, } fmt.Println(m) // make 定义 map
---

<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span><span style="color: #000000;">

func main() {

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> map
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 直接定义 map</span>
    m := map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">int</span><span style="color: #000000;"> {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">18</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800080;">11</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">otherName</span><span style="color: #800000;">"</span>:<span style="color: #800080;">12</span><span style="color: #000000;">,
    }
    fmt.Println(m)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> make 定义 map</span>
    m1 := make(map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">int</span>) <span style="color: #008000;">//</span><span style="color: #008000;"> m1 == empty map</span>
<span style="color: #000000;">    fmt.Println(m1)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var 定义 map</span>
    <span style="color: #0000ff;">var</span> m2 map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">int</span> <span style="color: #008000;">//</span><span style="color: #008000;"> m2 == nil</span>
<span style="color: #000000;">    fmt.Println(m2)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 遍历 map (不保证顺序)</span>
    <span style="color: #0000ff;">for</span> i,v :=<span style="color: #000000;"> range m {
        fmt.Println(i,v) </span><span style="color: #008000;">//</span><span style="color: #008000;"> i是key，v是value</span>
<span style="color: #000000;">    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 获取map里面键值</span>
    fmt.Println(m[<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">])
    fmt.Println(m[</span><span style="color: #800000;">"</span><span style="color: #800000;">ages</span><span style="color: #800000;">"</span>]) <span style="color: #008000;">//</span><span style="color: #008000;"> 若key不存在就会返回默认初始值

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 判断map里面key存不存在</span>
    <span style="color: #0000ff;">if</span> value,ok := m[<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">];ok {
        fmt.Println(</span><span style="color: #800000;">"</span><span style="color: #800000;">存在，值为：</span><span style="color: #800000;">"</span><span style="color: #000000;">,value)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除map里面的key</span>
    delete(m,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    fmt.Println(m)
}</span></pre>
</div>
<p>&nbsp;</p>
