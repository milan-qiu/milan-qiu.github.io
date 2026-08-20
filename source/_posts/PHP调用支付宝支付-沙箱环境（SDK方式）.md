---
title: "PHP调用支付宝支付-沙箱环境（SDK方式）"
date: "2020-06-17 00:36:00"
updated: "2020-06-17 14:09:00"
tags:
categories:
description: >-
  一、进入沙箱环境，获取环境的appid、支付宝网关 二、下载对应版本的SDK（以下为PHP版本）、解压到网站目录 1、http://p.tb.cn/rmsportal_6680_alipay.trade.wap.pay-PHP-UTF-8.zip 三、将沙箱的appid、支付宝网关填写到config
---

<p>一、进入沙箱环境，获取环境的appid、支付宝网关</p>
<p>&nbsp;</p>
<p>二、下载对应版本的SDK（以下为PHP版本）、解压到网站目录</p>
<p>1、<a href="http://p.tb.cn/rmsportal_6680_alipay.trade.wap.pay-PHP-UTF-8.zip" target="_blank">http://p.tb.cn/rmsportal_6680_alipay.trade.wap.pay-PHP-UTF-8.zip</a></p>
<p>&nbsp;</p>
<p>三、将沙箱的appid、支付宝网关填写到config文件中</p>
<p>&nbsp;</p>
<p>四、生成商户私钥和支付宝公钥</p>
<p>&nbsp;</p>
<p>五、下载windows密钥生成工具</p>
<p><a href="https://ideservice.alipay.com/ide/getPluginUrl.htm?clientType=assistant&amp;platform=win&amp;channelType=WEB" target="_blank">https://ideservice.alipay.com/ide/getPluginUrl.htm?clientType=assistant&amp;platform=win&amp;channelType=WEB</a></p>
<p>&nbsp;</p>
<p>六、运行，选择非java适用项，生成密钥，将商户私钥复制到config.php相应位置</p>
<p>&nbsp;</p>
<p>七、将公钥复制，到沙箱应用第三行，生成应用公钥，然后查看支付宝公钥</p>
<p>&nbsp;</p>
<p>八、将支付宝公钥复制到config.php文件中相应位置</p>
<p>&nbsp;</p>
<p>九、打开web站点</p>
<p>&nbsp;</p>
<p>十、下载沙箱钱包app，使用沙箱账号</p>
<p>&nbsp;</p>
<p>十一、支付时使用沙箱app支付即可</p>
<p>&nbsp;</p>
<p>注：真实环境中需要创建自己的应用，获取真实的appid等信息</p>
<p><a href="https://opensupport.alipay.com/support/helpcenter/190/201602469553?ant_source=antsupport">https://opensupport.alipay.com/support/helpcenter/190/201602469553?ant_source=antsupport</a></p>
