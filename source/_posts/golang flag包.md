---
title: "golang flag包"
date: "2022-09-08 16:40:00"
tags:
categories:
description: >-
  flag用于解析命令行选项 例子： package main import ( "fmt" "flag" ) var ( intflag int boolflag bool stringflag string ) // 初始化变量 func init() { flag.IntVar(&intflag
---

#### flag用于解析命令行选项

#### 例子：
```golang
package main

import (
  "fmt"
  "flag"
)

var (
  intflag int
  boolflag bool
  stringflag string
)

// 初始化变量
func init() {
  flag.IntVar(&intflag, "intflag", 0, "int flag value")
  flag.BoolVar(&boolflag, "boolflag", false, "bool flag value")
  flag.StringVar(&stringflag, "stringflag", "default", "string flag value")
}

func main() {
  // 将用户输入的变量解析为变量值
  flag.Parse()

  fmt.Println("int flag:", intflag)
  fmt.Println("bool flag:", boolflag)
  fmt.Println("string flag:", stringflag)
}
```

#### 使用：
显示帮助信息：
```sh
./main -h
```
<br>
输入变量并执行：

```sh
./main -intflag 1 -boolflag false -stringflag "haha"
```
