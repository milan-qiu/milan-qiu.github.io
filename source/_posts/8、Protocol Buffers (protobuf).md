---
title: "8、Protocol Buffers (protobuf)"
date: "2021-12-01 21:58:00"
updated: "2022-01-02 19:49:00"
tags:
categories:
description: >-
  安装 下载：https://github.com/protocolbuffers/protobuf/releases/tag/v3.19.1 解压到任意位置 设置path：D:\protoc-3.19.1\bin 添加 go 代码生成：https://github.com/grpc-ecosyste
---

<h2><strong>安装&nbsp;</strong></h2>
<p>下载：<a href="https://github.com/protocolbuffers/protobuf/releases/tag/v3.19.1" target="_blank">https://github.com/protocolbuffers/protobuf/releases/tag/v3.19.1</a></p>
<p>&nbsp;</p>
<p>解压到任意位置</p>
<p>&nbsp;</p>
<p>设置path：D:\protoc-3.19.1\bin</p>
<p>&nbsp;</p>
<p>添加 go 代码生成：<a href="https://github.com/grpc-ecosystem/grpc-gateway" target="_blank">https://github.com/grpc-ecosystem/grpc-gateway</a></p>
<p>&nbsp;</p>
<p>为 protoc 添加扩展</p>
<div class="cnblogs_code">
<p>go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-grpc-gateway@latest<br />go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2@latest<br />go install google.golang.org/protobuf/cmd/protoc-gen-go@latest<br />go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest</p>


</div>
<p>&nbsp;</p>
<p>复制 GOPATH 里面的&nbsp;D:\go\bin\bin\ 四个程序</p>
<p>到 GOROOT 里面&nbsp;C:\Users\Administrator\go\bin</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202112/1680452-20211202002652167-571221380.png" alt="" width="621" height="129" loading="lazy" /></p>
<p>&nbsp;</p>
<h2>简单使用</h2>
<p>书写 test.proto</p>
<div class="cnblogs_code">
<pre>syntax = <span style="color: #800000;">"</span><span style="color: #800000;">proto3</span><span style="color: #800000;">"</span>; <span style="color: #008000;">//</span><span style="color: #008000;"> 指定使用哪个版本</span>
<span style="color: #000000;">
package coolcar; </span><span style="color: #008000;">//</span><span style="color: #008000;"> 当前包名</span>
<span style="color: #000000;">
option go_package </span>= <span style="color: #800000;">"</span><span style="color: #800000;">ginStart/proto/goproto;testPackage</span><span style="color: #800000;">"</span>; <span style="color: #008000;">//</span><span style="color: #008000;"> 指定生成后的目录 ginStart/proto;   </span><span style="color: #008000;">//</span><span style="color: #008000;"> testPackage 指定生成后的包名</span>
<span style="color: #000000;">
message  Trip {
  </span><span style="color: #0000ff;">string</span> start = <span style="color: #800080;">1</span>;  <span style="color: #008000;">//</span><span style="color: #008000;"> 类型 字段名 = 第几个字段</span>
  <span style="color: #0000ff;">string</span>  end = <span style="color: #800080;">2</span><span style="color: #000000;">;
  int64 duiation_sec </span>= <span style="color: #800080;">3</span><span style="color: #000000;">;
  int64 fee_cent </span>= <span style="color: #800080;">4</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>书写 main.go&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
<span style="color: #000000;">
import testPackage </span><span style="color: #800000;">"</span><span style="color: #800000;">project/proto/goproto</span><span style="color: #800000;">"</span> <span style="color: #008000;">//</span><span style="color: #008000;"> project 表示go.mod定义的包名</span>
<span style="color: #000000;">
func main()  {
    trip :</span>=<span style="color: #000000;"> testPackage.Trip{
        Start: </span><span style="color: #800000;">"</span><span style="color: #800000;">aaa</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    }
    fmt.Println(</span>&amp;<span style="color: #000000;">trip)
}</span></pre>
</div>
<p>&nbsp;</p>
<p>创建 goproto 目录后</p>
<p>&nbsp;</p>
<p>在 .proto 文件的文件夹下，调用命令</p>
<div class="cnblogs_code">
<pre>protoc --go_out=goproto --go_opt=paths=source_relative test.proto</pre>
</div>
<p>&nbsp;</p>
<h3>JSON序列化 和 反序列化</h3>
<p>.proto</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">message Person {
  </span><span style="color: #0000ff;">string</span> name = <span style="color: #800080;">1</span><span style="color: #000000;">;
  int32 age </span>= <span style="color: #800080;">2</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>.go</p>
<div class="cnblogs_code">
<pre>    s :=<span style="color: #000000;"> testPackage.Person{
        Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">ss</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        Age: </span><span style="color: #800080;">11</span><span style="color: #000000;">,
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 序列化</span>
    b,err := proto.Marshal(&amp;<span style="color: #000000;">s)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">%X\n</span><span style="color: #800000;">"</span>,b) <span style="color: #008000;">//</span><span style="color: #008000;"> 0A027373100B
    </span><span style="color: #008000;">//</span><span style="color: #008000;">fmt.Println(b) </span><span style="color: #008000;">//</span><span style="color: #008000;"> [10 2 115 115 16 11]

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 反序列化</span>
    <span style="color: #0000ff;">var</span> temp testPackage.Person <span style="color: #008000;">//</span><span style="color: #008000;"> 定义哪个结构进行解码</span>
    err = proto.Unmarshal(b,&amp;temp) <span style="color: #008000;">//</span><span style="color: #008000;"> 将解码后的内容放进 temp</span>
    <span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    fmt.Println(</span>&amp;<span style="color: #000000;">temp)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将结构数据 转为 json字符串</span>
    b,err = json.Marshal(&amp;<span style="color: #000000;">temp)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">%s\n</span><span style="color: #800000;">"</span>,b)</pre>
</div>
<p>&nbsp;</p>
<h3>复合类型</h3>
<p>proto</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">message Person {
  </span><span style="color: #0000ff;">string</span> name = <span style="color: #800080;">1</span><span style="color: #000000;">;
  int32 age </span>= <span style="color: #800080;">2</span><span style="color: #000000;">;
}

message  Trip {
  </span><span style="color: #0000ff;">string</span> start = <span style="color: #800080;">1</span><span style="color: #000000;">;
  </span><span style="color: #0000ff;">string</span>  end = <span style="color: #800080;">2</span><span style="color: #000000;">;
  Person a </span>= <span style="color: #800080;">3</span><span style="color: #000000;">;
  Person b </span>= <span style="color: #800080;">4</span><span style="color: #000000;">;
  repeated Person c </span>= <span style="color: #800080;">5</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>调用</p>
<div class="cnblogs_code">
<pre>    trip :=<span style="color: #000000;"> testPackage.Trip{
        Start: </span><span style="color: #800000;">"</span><span style="color: #800000;">aaa</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        End: </span><span style="color: #800000;">"</span><span style="color: #800000;">bbb</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        A: </span>&amp;<span style="color: #000000;">testPackage.Person{
            Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">名字</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Age: </span><span style="color: #800080;">18</span><span style="color: #000000;">,
        },
        B: </span>&amp;<span style="color: #000000;">testPackage.Person{
            Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">另外名字</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Age: </span><span style="color: #800080;">20</span><span style="color: #000000;">,
        },
        C: []</span>*<span style="color: #000000;">testPackage.Person{
            {
                Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">11</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Age: </span><span style="color: #800080;">11</span><span style="color: #000000;">,
            },
            {
                Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">22</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Age: </span><span style="color: #800080;">22</span><span style="color: #000000;">,
            },
            {
                Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">22</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Age: </span><span style="color: #800080;">22</span><span style="color: #000000;">,
            },
        },
    }
    fmt.Println(</span>&amp;<span style="color: #000000;">trip)
</span><span style="color: #008000;">//</span><span style="color: #008000;">start:"aaa"  end:"bbb"  a:{name:"名字"  age:18}  b:{name:"另外名字"  age:20}  c:{name:"11"  age:11}  c:{name:"22"  age:22}  c:{name:"22"  age:22}</span></pre>
</div>
<p>&nbsp;</p>
<h3>枚举类型</h3>
<p>&nbsp;.proto</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">enum</span><span style="color: #000000;"> NowStatus {
  ONESTATUS </span>= <span style="color: #800080;">0</span><span style="color: #000000;">;
  TWOSTATUS </span>= <span style="color: #800080;">1</span><span style="color: #000000;">;
  THREESTATUS </span>= <span style="color: #800080;">2</span><span style="color: #000000;">;
  FOURSTATUS </span>= <span style="color: #800080;">3</span><span style="color: #000000;">;
}

message Person {
  </span><span style="color: #0000ff;">string</span> name = <span style="color: #800080;">1</span><span style="color: #000000;">;
  NowStatus status </span>= <span style="color: #800080;">2</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>使用</p>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;"> 直接使用</span>
    fmt.Println(testPackage.NowStatus_THREESTATUS) <span style="color: #008000;">//</span><span style="color: #008000;"> THREESTATUS</span>
    fmt.Println(testPackage.NowStatus(<span style="color: #800080;">2</span>)) <span style="color: #008000;">//</span><span style="color: #008000;"> THREESTATUS

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 混合使用</span>
    s :=<span style="color: #000000;"> testPackage.Person{
        Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">cc</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        Status: testPackage.NowStatus_THREESTATUS,
    }
    fmt.Println(</span>&amp;<span style="color: #000000;">s)
    </span><span style="color: #008000;">//</span><span style="color: #008000;">name:"cc"  status:THREESTATUS</span></pre>
</div>
<p>&nbsp;</p>
<h3>引用外部的proto文件</h3>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202201/1680452-20220102193621894-1014425859.png" alt="" width="467" height="168" loading="lazy" /></p>
<p>&nbsp;</p>
<h3>嵌套message</h3>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202201/1680452-20220102194733439-397102267.png" alt="" width="285" height="210" loading="lazy" /></p>
<p>&nbsp;</p>
<p>其他文件要使用 Result 的 struct，需要源码里搜索 Result</p>
<p>&nbsp;</p>
