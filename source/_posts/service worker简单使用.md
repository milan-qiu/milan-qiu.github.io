---
title: "service worker简单使用"
date: "2021-08-23 09:29:00"
tags:
categories:
description: >-
  index.html注册 var version = "2021/7/8 11:32:10"; //判断是否升级https var host = window.location.host; if(host=="" || host==""){ var http_equiv = document.que
---

<p>index.html注册</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">var</span> version = <span style="color: #800000;">"</span><span style="color: #800000;">2021/7/8 11:32:10</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        </span><span style="color: #008000;">//</span><span style="color: #008000;">判断是否升级https</span>
        <span style="color: #0000ff;">var</span> host =<span style="color: #000000;"> window.location.host;
        </span><span style="color: #0000ff;">if</span>(host==<span style="color: #800000;">"</span><span style="color: #800000;">"</span> || host==<span style="color: #800000;">"</span><span style="color: #800000;">"</span><span style="color: #000000;">){
            </span><span style="color: #0000ff;">var</span> http_equiv = document.querySelector(<span style="color: #800000;">'</span><span style="color: #800000;">meta[name=upHttps]</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            http_equiv.setAttribute(</span><span style="color: #800000;">"</span><span style="color: #800000;">http-equiv</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Content-Security-Policy</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            http_equiv.setAttribute(</span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">upgrade-insecure-requests</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        window.addEventListener(</span><span style="color: #800000;">'</span><span style="color: #800000;">load</span><span style="color: #800000;">'</span><span style="color: #000000;">, function () {
            </span><span style="color: #0000ff;">if</span> (<span style="color: #800000;">'</span><span style="color: #800000;">serviceWorker</span><span style="color: #800000;">'</span> <span style="color: #0000ff;">in</span><span style="color: #000000;"> navigator) {
                window._loadServiceWorker </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
                </span><span style="color: #008000;">//</span><span style="color: #008000;">直接更新sw触发</span>
                navigator.serviceWorker.addEventListener(<span style="color: #800000;">'</span><span style="color: #800000;">controllerchange</span><span style="color: #800000;">'</span><span style="color: #000000;">, function() {
                    </span><span style="color: #0000ff;">if</span> (app.deviceType != <span style="color: #800080;">3</span> &amp;&amp;<span style="color: #000000;"> app.index) {
                        app.showWarning(</span><span style="color: #800000;">"</span><span style="color: #800000;">APP有新的内容 &lt;br&gt; 请重启</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">确认</span><span style="color: #800000;">"</span><span style="color: #000000;">,function (){
                            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> window.location.reload();
                        })
                    }
                });

                </span><span style="color: #0000ff;">if</span> (host==<span style="color: #800000;">"</span><span style="color: #800000;">"</span> || host==<span style="color: #800000;">"</span><span style="color: #800000;">"</span><span style="color: #000000;">) {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">注册service worker</span>
                    navigator.serviceWorker.register(<span style="color: #800000;">'</span><span style="color: #800000;">./sw.js</span><span style="color: #800000;">'</span>, {scope: <span style="color: #800000;">'</span><span style="color: #800000;">./</span><span style="color: #800000;">'</span><span style="color: #000000;">})
                        .then(function (registration) {
                            </span><span style="color: #008000;">//</span><span style="color: #008000;"> console.log(`${registration.scope} 成功注册了service worker`);
                            </span><span style="color: #008000;">//</span><span style="color: #008000;"> alert('sw注册成功')</span>
<span style="color: #000000;">                        })
                        .</span><span style="color: #0000ff;">catch</span><span style="color: #000000;">(function (err) {
                            console.log(</span><span style="color: #800000;">'</span><span style="color: #800000;">service worker注册失败：</span><span style="color: #800000;">'</span><span style="color: #000000;">, err);
                            </span><span style="color: #008000;">//</span><span style="color: #008000;"> alert('service worker注册失败：' + err)</span>
<span style="color: #000000;">                        });
                } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">卸载service worker</span>
<span style="color: #000000;">                    navigator.serviceWorker.getRegistrations()
                        .then( registrations </span>=&gt;<span style="color: #000000;"> {
                            </span><span style="color: #0000ff;">for</span><span style="color: #000000;">(let registration of registrations) {
                                registration.unregister()
                            }
                        })
                        .</span><span style="color: #0000ff;">catch</span>(err =&gt;<span style="color: #000000;"> {
                            console.log(</span><span style="color: #800000;">'</span><span style="color: #800000;">service worker卸载失败</span><span style="color: #800000;">'</span><span style="color: #000000;">, err)
                        })
                }

            }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 如果浏览器不支持service worker</span>
                window._loadServiceWorker = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
                top.postMessage(JSON.stringify({
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">action</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">CheckAppReloads</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">: [version]
                }), </span><span style="color: #800000;">'</span><span style="color: #800000;">*</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            }
        })</span></pre>
</div>
<p>&nbsp;</p>
<p>sw.js配置文件</p>
<div class="cnblogs_code">
<pre>let cacheName = <span style="color: #800000;">"</span><span style="color: #800000;">2021/8/19 15:41:24</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 缓存文件列表</span>
<span style="color: #0000ff;">const</span> cacheList =<span style="color: #000000;"> [
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 基本缓存文件
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> './public/image/favicon.jpg',
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> './assets/plugin/cannan/animate.css',
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> './assets/plugin/cannan/canaan.css',
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> './assets/plugin/cannan/canaan.div.release.js',
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> './assets/plugin/weixin-js-sdk/jweixin-1.6.0.js'</span>
<span style="color: #000000;">]

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 执行缓存操作</span>
<span style="color: #0000ff;">this</span>.addEventListener(<span style="color: #800000;">'</span><span style="color: #800000;">install</span><span style="color: #800000;">'</span>, <span style="color: #0000ff;">event</span> =&gt;<span style="color: #000000;"> {
    </span><span style="color: #0000ff;">this</span>.skipWaiting()<span style="color: #008000;">//</span><span style="color: #008000;"> 装完直接用</span>

    <span style="color: #0000ff;">event</span><span style="color: #000000;">.waitUntil(

        caches.open(cacheName).then(cache </span>=&gt;<span style="color: #000000;"> {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (cache) cache.addAll(cacheList)
        }).</span><span style="color: #0000ff;">catch</span>(e =&gt;<span style="color: #000000;"> {
            console.log(e)
        })
    )
})

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 激活。清空上个service worker保存的内容</span>
<span style="color: #0000ff;">this</span>.addEventListener(<span style="color: #800000;">'</span><span style="color: #800000;">activate</span><span style="color: #800000;">'</span>, <span style="color: #0000ff;">event</span> =&gt;<span style="color: #000000;"> {
    </span><span style="color: #0000ff;">event</span><span style="color: #000000;">.waitUntil(

        caches.keys().then((nameList) </span>=&gt;<span style="color: #000000;"> {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Promise.all(
                nameList.map((i) </span>=&gt;<span style="color: #000000;"> {
                    </span><span style="color: #0000ff;">if</span> (i !==<span style="color: #000000;"> cacheName) {
                        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> caches.delete(i)
                    }
                })
            )

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> for(var i = 0; i &lt; nameList.length; i++){
            </span><span style="color: #008000;">//</span><span style="color: #008000;">     if(i !== cacheName) caches.delete(i);
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> }</span>
        }).<span style="color: #0000ff;">catch</span>(e =&gt;<span style="color: #000000;"> console.log(e))
    )
})

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 监听请求</span>
<span style="color: #0000ff;">this</span>.addEventListener(<span style="color: #800000;">'</span><span style="color: #800000;">fetch</span><span style="color: #800000;">'</span>, <span style="color: #0000ff;">event</span> =&gt;<span style="color: #000000;"> {
    </span><span style="color: #0000ff;">event</span><span style="color: #000000;">.respondWith(

        caches.match(</span><span style="color: #0000ff;">event</span><span style="color: #000000;">.request)

            .then(res </span>=&gt;<span style="color: #000000;"> {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 匹配到缓存直接返回</span>
                <span style="color: #0000ff;">if</span> (res) <span style="color: #0000ff;">return</span><span style="color: #000000;"> res

                </span><span style="color: #0000ff;">const</span> requestClone = <span style="color: #0000ff;">event</span>.request.clone() <span style="color: #008000;">//</span><span style="color: #008000;"> 复制请求头

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 直接请求，并返回
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> return fetch(requestClone).then(new_res =&gt; new_res)

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 直接请求，缓存后返回</span>
                <span style="color: #0000ff;">return</span> fetch(requestClone).then(new_res =&gt;<span style="color: #000000;"> {
                    </span><span style="color: #0000ff;">if</span> (!new_res || new_res.status !== <span style="color: #800080;">200</span>) <span style="color: #0000ff;">return</span> new_res <span style="color: #008000;">//</span><span style="color: #008000;"> 响应报错，直接返回</span>

                    <span style="color: #0000ff;">const</span> responseClone = new_res.clone() <span style="color: #008000;">//</span><span style="color: #008000;"> 复制响应

                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 除了php, html, application, json 不缓存，其他都缓存</span>
                    <span style="color: #0000ff;">const</span> pattern = /\.php|bj-admin|sockjs-node|upload|uid|sentry|sw\.js/<span style="color: #000000;">ig

                    </span><span style="color: #0000ff;">if</span> (!pattern.test(new_res.url)) { caches.open(cacheName).then(cache =&gt; cache &amp;&amp; cache.put(requestClone, responseClone)).<span style="color: #0000ff;">catch</span>(e =&gt; console.log(e)) } <span style="color: #008000;">//</span><span style="color: #008000;"> 进行缓存</span>

                    <span style="color: #0000ff;">return</span><span style="color: #000000;"> new_res
                }).</span><span style="color: #0000ff;">catch</span>(e =&gt;<span style="color: #000000;"> {
                    console.log(e)
                })
            }).</span><span style="color: #0000ff;">catch</span>(e =&gt;<span style="color: #000000;"> {
                console.log(e)
            })
    )
})</span></pre>
</div>
<p>&nbsp;</p>
