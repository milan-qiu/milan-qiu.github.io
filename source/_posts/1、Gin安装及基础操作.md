---
title: "1、Gin安装及基础操作"
date: "2022-02-24 19:03:00"
tags:
categories:
description: >-
  安装：go get -u github.com/gin-gonic/gin 初始化：go mod init project 使用示例 package main import "github.com/gin-gonic/gin" func main() { r := gin.Default() //
---

<p>安装：go get <span class="token operator">-u github<span class="token punctuation">.com<span class="token operator">/gin<span class="token operator">-gonic<span class="token operator">/gin</span></span></span></span></span></p>
<p>&nbsp;</p>
<p><span class="token operator"><span class="token punctuation"><span class="token operator"><span class="token operator"><span class="token operator">初始化：go mod init project</span></span></span></span></span></p>
<p>&nbsp;</p>
<p><span class="token operator"><span class="token punctuation"><span class="token operator"><span class="token operator"><span class="token operator">使用示例</span></span></span></span></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import </span><span style="color: #800000;">"</span><span style="color: #800000;">github.com/gin-gonic/gin</span><span style="color: #800000;">"</span><span style="color: #000000;">

func main() {
    r :</span>=<span style="color: #000000;"> gin.Default()  // 比 gin.New 多了 logger 和 recovery （crash-fee）中间件
    r.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span>, func(c *<span style="color: #000000;">gin.Context) {
        c.JSON(</span><span style="color: #800080;">200</span><span style="color: #000000;">, gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">message</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">pong</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        })
    })
    r.Run() </span><span style="color: #008000;">//</span><span style="color: #008000;"> listen and serve on 0.0.0.0:8080</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>不同的请求方式</h3>
<div class="cnblogs_code">
<pre>func res(c *<span style="color: #000000;">gin.Context) {
    c.JSON(</span><span style="color: #800080;">200</span><span style="color: #000000;">, gin.H{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">message</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">pong</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    })
}

func main() {
    r :</span>=<span style="color: #000000;"> gin.Default()

    r.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span><span style="color: #000000;">, res)
    r.POST(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)
    r.PUT(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)
    r.DELETE(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)
    r.PATCH(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)
    r.HEAD(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)
    r.OPTIONS(</span><span style="color: #800000;">"</span><span style="color: #800000;">/ping</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)

    r.Run(</span><span style="color: #800000;">"</span><span style="color: #800000;">:7777</span><span style="color: #800000;">"</span>) <span style="color: #008000;">//</span><span style="color: #008000;"> 默认8080</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>路由分组</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">func main() {
    r :</span>=<span style="color: #000000;"> gin.Default()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 路由分组</span>
    group1 := r.Group(<span style="color: #800000;">"</span><span style="color: #800000;">/goods</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    group1.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">ping</span><span style="color: #800000;">"</span>,res) <span style="color: #008000;">//</span><span style="color: #008000;"> 能通过 /goods/ping 访问

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 路由分组（正常书写模式）</span>
    group2 := r.Group(<span style="color: #800000;">"</span><span style="color: #800000;">list</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    {
        group2.HEAD(</span><span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)
        group2.POST(</span><span style="color: #800000;">"</span><span style="color: #800000;">otherItem</span><span style="color: #800000;">"</span><span style="color: #000000;">,res)
    }
    
    r.Run()
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>uri 地址变量获取</h3>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;"> 动态路由</span>
    r.GET(<span style="color: #800000;">"</span><span style="color: #800000;">/book/:id</span><span style="color: #800000;">"</span>, func(c *gin.Context) { <span style="color: #008000;">//</span><span style="color: #008000;"> 变量可以在后面、中间、前面</span>
        id := c.Param(<span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span>) <span style="color: #008000;">//</span><span style="color: #008000;"> 获取url上的变量</span>
<span style="color: #000000;">        c.JSON(http.StatusOK, gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">key</span><span style="color: #800000;">"</span><span style="color: #000000;"> : id,
        })
    })

    r.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/shoes/:item/:ott</span><span style="color: #800000;">"</span>, func(c *gin.Context) { <span style="color: #008000;">//</span><span style="color: #008000;"> 可以有两个变量</span>
<span style="color: #000000;">        c.JSON(http.StatusOK, gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : c.Param(<span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span><span style="color: #000000;">),
            </span><span style="color: #800000;">"</span><span style="color: #800000;">ott</span><span style="color: #800000;">"</span> : c.Param(<span style="color: #800000;">"</span><span style="color: #800000;">ott</span><span style="color: #800000;">"</span><span style="color: #000000;">),
        })
    })

    r.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">/url/*pp</span><span style="color: #800000;">"</span>, func(c *gin.Context) { <span style="color: #008000;">//</span><span style="color: #008000;"> 获取 /url 后面所有的内容</span>
<span style="color: #000000;">        c.JSON(http.StatusOK, gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">item111</span><span style="color: #800000;">"</span> : c.Param(<span style="color: #800000;">"</span><span style="color: #800000;">pp</span><span style="color: #800000;">"</span><span style="color: #000000;">),
        })
    })</span></pre>
</div>
<p>&nbsp;</p>
<h3>约束 uri 地址变量</h3>
<div class="cnblogs_code">
<pre>    type Person <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
        Name </span><span style="color: #0000ff;">string</span>    `uri:<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> binding:<span style="color: #800000;">"</span><span style="color: #800000;">required</span><span style="color: #800000;">"</span><span style="color: #000000;">`
        Age </span><span style="color: #0000ff;">int</span>    `uri:<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span> binding:<span style="color: #800000;">"</span><span style="color: #800000;">required</span><span style="color: #800000;">"</span><span style="color: #000000;">`
    }

    r.GET(</span><span style="color: #800000;">"</span><span style="color: #800000;">judge/:name/:age</span><span style="color: #800000;">"</span>, func(c *<span style="color: #000000;">gin.Context) {
        name :</span>= c.Param(<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        age :</span>= c.Param(<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">)

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 处理错误的传值</span>
        <span style="color: #0000ff;">var</span><span style="color: #000000;"> person Person
        </span><span style="color: #0000ff;">if</span> err := c.ShouldBindUri(&amp;person); err !=<span style="color: #000000;"> nil {
            c.JSON(http.StatusNotFound,gin.H{
                </span><span style="color: #800000;">"</span><span style="color: #800000;">status</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">404</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            })
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">
        }

        c.JSON(http.StatusOK,gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;"> : name,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;"> : age,
        })
    })</span></pre>
</div>
<p>&nbsp;</p>
<h3>获取 请求参数</h3>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;"> 从 get 获取参数</span>
    r.GET(<span style="color: #800000;">"</span><span style="color: #800000;">/welcome</span><span style="color: #800000;">"</span>, func(c *<span style="color: #000000;">gin.Context) {

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 带默认值方式</span>
        dd := c.DefaultQuery(<span style="color: #800000;">"</span><span style="color: #800000;">dd</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">i am dd</span><span style="color: #800000;">"</span><span style="color: #000000;">)

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 不带默认值方式</span>
        cc := c.Query(<span style="color: #800000;">"</span><span style="color: #800000;">cc</span><span style="color: #800000;">"</span><span style="color: #000000;">)

        c.JSON(http.StatusOK, gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">dd</span><span style="color: #800000;">"</span><span style="color: #000000;"> : dd,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">cc</span><span style="color: #800000;">"</span><span style="color: #000000;"> : cc,
        })
    })

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 从 post 获取参数</span>
    r.POST(<span style="color: #800000;">"</span><span style="color: #800000;">/welcome-post</span><span style="color: #800000;">"</span>, func(c *<span style="color: #000000;">gin.Context) {

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 带默认值方式</span>
        dd := c.DefaultPostForm(<span style="color: #800000;">"</span><span style="color: #800000;">dd</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">i am dd</span><span style="color: #800000;">"</span><span style="color: #000000;">)

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 不带默认值方式</span>
        cc := c.PostForm(<span style="color: #800000;">"</span><span style="color: #800000;">cc</span><span style="color: #800000;">"</span><span style="color: #000000;">)

        c.JSON(http.StatusOK, gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">dd</span><span style="color: #800000;">"</span><span style="color: #000000;"> : dd,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">cc</span><span style="color: #800000;">"</span><span style="color: #000000;"> : cc,
        })
    })</span></pre>
</div>
<p>&nbsp;</p>
<h3>表单验证</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/gin-gonic/gin</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">net/http</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 内置表单验证用的包：</span><span style="color: #008000; text-decoration: underline;">https://github.com/go-playground/validator</span>

<span style="color: #008000;">//</span><span style="color: #008000;"> LoginForm 定义表单字段的规则</span>
type LoginForm <span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    User </span><span style="color: #0000ff;">string</span> `json:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span> binding:<span style="color: #800000;">"</span><span style="color: #800000;">required,min=3,max=10</span><span style="color: #800000;">"</span><span style="color: #000000;">`
    Password </span><span style="color: #0000ff;">string</span> `json:<span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span> binding:<span style="color: #800000;">"</span><span style="color: #800000;">required</span><span style="color: #800000;">"</span><span style="color: #000000;">`
}

type SignTest </span><span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    User </span><span style="color: #0000ff;">string</span> `json:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span> binding:<span style="color: #800000;">"</span><span style="color: #800000;">required,min=3,max=10</span><span style="color: #800000;">"</span><span style="color: #000000;">`
    Password </span><span style="color: #0000ff;">string</span> `json:<span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span> binding:<span style="color: #800000;">"</span><span style="color: #800000;">required</span><span style="color: #800000;">"</span><span style="color: #000000;">`
    RePassword </span><span style="color: #0000ff;">string</span> `json:<span style="color: #800000;">"</span><span style="color: #800000;">re-password</span><span style="color: #800000;">"</span> binding:<span style="color: #800000;">"</span><span style="color: #800000;">required,eqfield=Password</span><span style="color: #800000;">"</span>` <span style="color: #008000;">//</span><span style="color: #008000;"> eqfielf 表明该字段数据和 xxx 数据一样</span>
<span style="color: #000000;">}

func main() {
    r :</span>=<span style="color: #000000;"> gin.Default()

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 登录验证</span>
    r.POST(<span style="color: #800000;">"</span><span style="color: #800000;">/testForm</span><span style="color: #800000;">"</span>, func(c *<span style="color: #000000;">gin.Context) {

        </span><span style="color: #0000ff;">var</span><span style="color: #000000;"> loginForm LoginForm

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 验证不通过就</span>
        <span style="color: #0000ff;">if</span> err := c.ShouldBind(&amp;loginForm); err !=<span style="color: #000000;"> nil {
            fmt.Println(err.Error())
            c.JSON(http.StatusBadRequest,gin.H{
                </span><span style="color: #800000;">"</span><span style="color: #800000;">error</span><span style="color: #800000;">"</span><span style="color: #000000;"> : err.Error(),
            })
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 通过就</span>
<span style="color: #000000;">        c.JSON(http.StatusOK,gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">message</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">success login</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        })
    })

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册验证</span>
    r.POST(<span style="color: #800000;">"</span><span style="color: #800000;">/signup</span><span style="color: #800000;">"</span>, func(c *<span style="color: #000000;">gin.Context) {

        </span><span style="color: #0000ff;">var</span><span style="color: #000000;"> signT SignTest

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 验证不通过就</span>
        <span style="color: #0000ff;">if</span> err := c.ShouldBind(&amp;signT); err !=<span style="color: #000000;"> nil {
            fmt.Println(err.Error())
            c.JSON(http.StatusBadRequest,gin.H{
                </span><span style="color: #800000;">"</span><span style="color: #800000;">error</span><span style="color: #800000;">"</span><span style="color: #000000;"> : err.Error(),
            })
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 通过就</span>
<span style="color: #000000;">        c.JSON(http.StatusOK,gin.H{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">message</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">success register</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        })
    })

    r.Run()
}</span></pre>
</div>
<p>&nbsp;</p>
