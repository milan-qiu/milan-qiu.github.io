---
title: "1、自动迁移（AutoMigrate）"
date: "2022-01-09 21:15:00"
tags:
categories:
description: >-
  package main import ( "gorm.io/driver/mysql" "gorm.io/gorm" "gorm.io/gorm/logger" "log" "os" "time" ) type table1 struct { gorm.Model Name string Age
---

<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">gorm.io/driver/mysql</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">gorm.io/gorm</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">gorm.io/gorm/logger</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">log</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">os</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">time</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

type table1 </span><span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    gorm.Model
    Name </span><span style="color: #0000ff;">string</span><span style="color: #000000;">
    Age </span><span style="color: #0000ff;">uint</span><span style="color: #000000;">
}

func main() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 初始化日志</span>
    newLogger :=<span style="color: #000000;"> logger.New(
        log.New(os.Stdout, </span><span style="color: #800000;">"</span><span style="color: #800000;">\r\n</span><span style="color: #800000;">"</span>, log.LstdFlags), <span style="color: #008000;">//</span><span style="color: #008000;"> io writer（日志输出的目标，前缀和日志包含的内容&mdash;&mdash;译者注）</span>
<span style="color: #000000;">        logger.Config{
            SlowThreshold: time.Second,   </span><span style="color: #008000;">//</span><span style="color: #008000;"> 慢 SQL 阈值</span>
            LogLevel:      logger.Info, <span style="color: #008000;">//</span><span style="color: #008000;"> 日志级别</span>
            IgnoreRecordNotFoundError: <span style="color: #0000ff;">true</span>,   <span style="color: #008000;">//</span><span style="color: #008000;"> 忽略ErrRecordNotFound（记录未找到）错误</span>
            Colorful:      <span style="color: #0000ff;">true</span>,         <span style="color: #008000;">//</span><span style="color: #008000;"> 禁用彩色打印</span>
<span style="color: #000000;">        },
    )

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 数据库配置信息</span>
    dsn := <span style="color: #800000;">"</span><span style="color: #800000;">root:root@tcp(127.0.0.1:3306)/gorm?charset=utf8mb4&amp;parseTime=True&amp;loc=Local</span><span style="color: #800000;">"</span>

    <span style="color: #008000;">//</span><span style="color: #008000;"> 建立数据库链接</span>
    db, _ := gorm.Open(mysql.Open(dsn), &amp;<span style="color: #000000;">gorm.Config{
        Logger: newLogger,
    })

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 开始做自动迁移</span>
    _ = db.AutoMigrate(&amp;<span style="color: #000000;">table1{})
}</span></pre>
</div>
<p>&nbsp;</p>
<p>打印的日志信息</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202201/1680452-20220109211325562-1398891135.png" alt="" width="1196" height="245" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>生成的数据表</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202201/1680452-20220109211423375-1503826650.png" alt="" width="713" height="228" loading="lazy" /></p>
<p>&nbsp;</p>
