---
title: "jeager 链路追踪功能"
date: "2022-03-13 14:33:00"
updated: "2022-03-13 21:19:00"
tags:
categories:
description: >-
  官方文档 all in one 安装 docker run -d --name jaeger \ -e COLLECTOR_ZIPKIN_HOST_PORT=:9411 \ -p 5775:5775/udp \ -p 6831:6831/udp \ -p 6832:6832/udp \ -p 577
---

<p><a href="https://github.com/jaegertracing/jaeger" target="_blank">官方文档</a></p>
<p>&nbsp;</p>
<p>all in one 安装</p>
<div class="cnblogs_code">
<pre>docker run -d --<span style="color: #000000;">name jaeger \
  </span>-e COLLECTOR_ZIPKIN_HOST_PORT=:<span style="color: #800080;">9411</span><span style="color: #000000;"> \
  </span>-p <span style="color: #800080;">5775</span>:<span style="color: #800080;">5775</span>/<span style="color: #000000;">udp \
  </span>-p <span style="color: #800080;">6831</span>:<span style="color: #800080;">6831</span>/<span style="color: #000000;">udp \
  </span>-p <span style="color: #800080;">6832</span>:<span style="color: #800080;">6832</span>/<span style="color: #000000;">udp \
  </span>-p <span style="color: #800080;">5778</span>:<span style="color: #800080;">5778</span><span style="color: #000000;"> \
  </span>-p <span style="color: #800080;">16686</span>:<span style="color: #800080;">16686</span><span style="color: #000000;"> \
  </span>-p <span style="color: #800080;">14250</span>:<span style="color: #800080;">14250</span><span style="color: #000000;"> \
  </span>-p <span style="color: #800080;">14268</span>:<span style="color: #800080;">14268</span><span style="color: #000000;"> \
  </span>-p <span style="color: #800080;">14269</span>:<span style="color: #800080;">14269</span><span style="color: #000000;"> \
  </span>-p <span style="color: #800080;">9411</span>:<span style="color: #800080;">9411</span><span style="color: #000000;"> \
  jaegertracing</span>/all-<span style="color: #0000ff;">in</span>-one:<span style="color: #800080;">1.32</span></pre>
</div>
<p>&nbsp;</p>
<p>或者正常安装</p>
<div class="cnblogs_code">
<pre>docker run --rm -<span style="color: #000000;">it \
  </span>--<span style="color: #000000;">link jaeger \
  </span>-p8080-<span style="color: #800080;">8083</span>:<span style="color: #800080;">8080</span>-<span style="color: #800080;">8083</span><span style="color: #000000;"> \
  </span>-e JAEGER_AGENT_HOST=<span style="color: #800000;">"</span><span style="color: #800000;">jaeger</span><span style="color: #800000;">"</span><span style="color: #000000;"> \
  jaegertracing</span>/example-hotrod:<span style="color: #800080;">1.32</span><span style="color: #000000;"> \
  all</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><a href="http://localhost:16686/" target="_blank">jaeger ui 访问&nbsp;http://localhost:16686/</a></p>
