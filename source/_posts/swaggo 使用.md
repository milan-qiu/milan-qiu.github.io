---
title: "swaggo 使用"
date: "2022-03-08 18:12:00"
updated: "2022-03-08 18:53:00"
tags:
categories:
description: >-
  官方文档 本地安装 go install github.com/swaggo/swag/cmd/swag@latest 项目依赖包 go get github.com/swaggo/gin-swagger go get github.com/swaggo/files main.go package
---

<p><a href="https://github.com/swaggo/swag/blob/master/README_zh-CN.md#%E5%A6%82%E4%BD%95%E4%B8%8Egin%E9%9B%86%E6%88%90" target="_blank">官方文档</a></p>
<p>&nbsp;</p>
<p>本地安装</p>
<div class="cnblogs_code">
<pre>go install github.com/swaggo/swag/cmd/swag@latest</pre>
</div>
<p>&nbsp;</p>
<p>项目依赖包</p>
<div class="cnblogs_code">
<pre>go <span style="color: #0000ff;">get</span> github.com/swaggo/gin-<span style="color: #000000;">swagger
go </span><span style="color: #0000ff;">get </span><span class="pl-s">github.com/swaggo/files</span></pre>
</div>
<p>&nbsp;</p>
<p>main.go</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">net/http</span><span style="color: #800000;">"</span>

    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/gin-gonic/gin</span><span style="color: #800000;">"</span><span style="color: #000000;">
    swaggerFiles </span><span style="color: #800000;">"</span><span style="color: #800000;">github.com/swaggo/files</span><span style="color: #800000;">"</span><span style="color: #000000;">
    ginSwagger </span><span style="color: #800000;">"</span><span style="color: #800000;">github.com/swaggo/gin-swagger</span><span style="color: #800000;">"</span><span style="color: #000000;">

    _ </span><span style="color: #800000;">"</span><span style="color: #800000;">jwt/docs</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

</span><span style="color: #008000;">//</span><span style="color: #008000;"> @title Swagger Example API
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @version 1.0
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @description This is a sample server celler server.
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @termsOfService </span><span style="color: #008000; text-decoration: underline;">https://www.topgoer.com</span>

<span style="color: #008000;">//</span><span style="color: #008000;"> @contact.name www.topgoer.com
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @contact.url </span><span style="color: #008000; text-decoration: underline;">https://www.topgoer.com</span>
<span style="color: #008000;">//</span><span style="color: #008000;"> @contact.email me@razeen.me

</span><span style="color: #008000;">//</span><span style="color: #008000;"> @license.name Apache 2.0
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @license.url </span><span style="color: #008000; text-decoration: underline;">http://www.apache.org/licenses/LICENSE-2.0.html</span>

<span style="color: #008000;">//</span><span style="color: #008000;"> @host 127.0.0.1:8080
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @BasePath /api/v1</span>
<span style="color: #000000;">
func main() {

    r :</span>=<span style="color: #000000;"> gin.Default()

    v1 :</span>= r.Group(<span style="color: #800000;">"</span><span style="color: #800000;">/api/v1</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    {
        v1.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/hello</span><span style="color: #800000;">"</span><span style="color: #000000;">, HandleHello)
        v1.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/hi</span><span style="color: #800000;">"</span><span style="color: #000000;">, HandleHi)
    }

    r.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/hello</span><span style="color: #800000;">"</span><span style="color: #000000;">,HandleHello)

    r.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/swagger/*any</span><span style="color: #800000;">"</span><span style="color: #000000;">, ginSwagger.WrapHandler(swaggerFiles.Handler))

    r.Run(</span><span style="color: #800000;">"</span><span style="color: #800000;">:8080</span><span style="color: #800000;">"</span><span style="color: #000000;">)
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> HandleHi  @Summary 测试SayHello
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Description 向你说Hello
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Tags 我是标签
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Accept json
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Param who query string true "人名"
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Router /hi [get]</span>
func HandleHi(c *<span style="color: #000000;">gin.Context) {
    c.JSON(http.StatusOK,gin.H{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">msg</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hello</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    })
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> HandleHello @Summary 测试SayHello
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Description 向你说Hello
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Tags 测试
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Accept json
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Param who query string true "人名"
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Success 200 {string} string "{"msg": "hello Razeen"}"
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Failure 400 {string} string "{"msg": "who are you"}"
</span><span style="color: #008000;">//</span><span style="color: #008000;"> @Router /hello [get]</span>
func HandleHello(c *<span style="color: #000000;">gin.Context) {
    c.JSON(http.StatusOK,gin.H{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">msg</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hello</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    })
}</span></pre>
</div>
<p>&nbsp;</p>
<p>生成或更新swagger文档</p>
<div class="cnblogs_code">
<pre>swag init</pre>
</div>
<p>&nbsp;</p>
<p>运行 gin</p>
<div class="cnblogs_code">
<pre>go run .</pre>
</div>
<p>&nbsp;</p>
<p>查看swagger文档</p>
<p><a href="http://localhost:8080/swagger/index.html" target="_blank">http://localhost:8080/swagger/index.html</a></p>
<p>&nbsp;</p>
<p>TODO: 通过 build tag 控制最后的打包（go build -tags="doc"）</p>
