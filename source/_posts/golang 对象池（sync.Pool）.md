---
title: "golang 对象池（sync.Pool）"
date: "2022-09-08 14:39:00"
tags:
categories:
description: >-
  作用：保存和复用临时对象，减少内存分配，降低 GC 压力。 正常代码： type Student struct { Name string Age int32 Remark [1024]byte } var buf, _ = json.Marshal(Student{Name: "Geektutu"
---

##### 作用：保存和复用临时对象，减少内存分配，降低 GC 压力。

#### 正常代码：
```golang
type Student struct {
	Name   string
	Age    int32
	Remark [1024]byte
}

var buf, _ = json.Marshal(Student{Name: "Geektutu", Age: 25})

func unmarsh() {
	stu := &Student{}
	json.Unmarshal(buf, stu)
}
```

#### 使用对象池代码：
```golang
type Student struct {
	Name   string
	Age    int32
	Remark [1024]byte
}

var studentPool = sync.Pool{
    New: func() interface{} { 
        return new(Student) 
    },
}

stu := studentPool.Get().(*Student)
json.Unmarshal(buf, stu)
studentPool.Put(stu)
```
