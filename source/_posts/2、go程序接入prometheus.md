---
title: "2、go程序接入prometheus"
date: "2023-05-02 12:18:00"
tags:
categories:
description: >-
  参考：https://prometheus.io/docs/guides/go-application/ go默认基础指标 package main import ( "net/http" "github.com/prometheus/client_golang/prometheus/promhtt
---

参考：https://prometheus.io/docs/guides/go-application/
### go默认基础指标
```golang
package main

import (
	"net/http"

	"github.com/prometheus/client_golang/prometheus/promhttp"
)

func main() {
	http.Handle("/metrics", promhttp.Handler())
	http.ListenAndServe(":2112", nil)
}
```

### go自定义指标
```golang
package main

import (
        "net/http"
        "time"

        "github.com/prometheus/client_golang/prometheus"
        "github.com/prometheus/client_golang/prometheus/promauto"
        "github.com/prometheus/client_golang/prometheus/promhttp"
)

func recordMetrics() {
        go func() {
                for {
                        opsProcessed.Inc()
                        time.Sleep(2 * time.Second)
                }
        }()
}

var (
        opsProcessed = promauto.NewCounter(prometheus.CounterOpts{
                Name: "myapp_processed_ops_total",
                Help: "The total number of processed events",
        })
)

func main() {
        recordMetrics()

        http.Handle("/metrics", promhttp.Handler())
        http.ListenAndServe(":2112", nil)
}
```
后续在prometheus接入datasource、dashboard即可查看信息

分布式go程序，需要prometheus配置服务发现机制
可参考：
https://prometheus.io/docs/guides/file-sd/
https://prometheus.io/docs/prometheus/latest/configuration/configuration/#consul_sd_config
