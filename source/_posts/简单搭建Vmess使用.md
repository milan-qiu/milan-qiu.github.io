---
title: "简单搭建Vmess使用"
date: "2021-02-28 15:17:00"
tags:
categories:
description: >-
  安装脚本 查看id cat /proc/sys/kernel/random/uuid 编辑配置文件 主要编辑端口、id { "inbounds": [{ "port": 2088, "protocol": "vmess", "settings": { "clients": [ { "id": "9e
---

<p>安装脚本</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210228151641002-1694226764.png" alt="" width="766" height="46" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>查看id</p>
<div class="cnblogs_code">
<pre>cat /proc/sys/kernel/random/uuid</pre>
</div>
<p>&nbsp;</p>
<p>编辑配置文件</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210228151559075-219569126.png" alt="" width="398" height="50" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>主要编辑端口、id</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">inbounds</span><span style="color: #800000;">"</span><span style="color: #000000;">: [{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">port</span><span style="color: #800000;">"</span>: <span style="color: #800080;">2088</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">protocol</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">vmess</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">clients</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
        {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">9ec43ee9-651d-435d-ac8f-c06dtfc79b01</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">level</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">alterId</span><span style="color: #800000;">"</span>: <span style="color: #800080;">64</span><span style="color: #000000;">
        }
      ]
    }
  }],
  </span><span style="color: #800000;">"</span><span style="color: #800000;">outbounds</span><span style="color: #800000;">"</span><span style="color: #000000;">: [{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">protocol</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">freedom</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}
  },{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">protocol</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">blackhole</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {},
    </span><span style="color: #800000;">"</span><span style="color: #800000;">tag</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">blocked</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }],
  </span><span style="color: #800000;">"</span><span style="color: #800000;">routing</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">rules</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
      {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">ip</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">geoip:private</span><span style="color: #800000;">"</span><span style="color: #000000;">],
        </span><span style="color: #800000;">"</span><span style="color: #800000;">outboundTag</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">blocked</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    ]
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>开启服务及简单命令&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210228151326299-1726257220.png" alt="" width="406" height="173" loading="lazy" /></p>
<p>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202102/1680452-20210228150931731-1969825198.png" alt="" width="685" height="558" loading="lazy" /></p>
<p>&nbsp;</p>
