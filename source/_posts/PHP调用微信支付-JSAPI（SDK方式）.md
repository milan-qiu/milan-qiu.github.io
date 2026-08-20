---
title: "PHP调用微信支付-JSAPI（SDK方式）"
date: "2020-06-16 23:16:00"
updated: "2020-06-17 13:43:00"
tags:
categories:
description: >-
  准备一、设置支付目录 https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3 准备二、设置授权域名 1、 https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3 2、下
---

<p>准备一、设置支付目录</p>
<p><a href="https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3">https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3</a></p>
<p>&nbsp;</p>
<p>准备二、设置授权域名</p>
<p>1、&nbsp;<a href="https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3">https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3</a></p>
<p>2、下载回调文件(.txt)，上传到网站根目录</p>
<p>&nbsp;</p>
<p>一、获取AppID、AppSecret</p>
<p>1、APPID：绑定支付的APPID（必须配置，开户邮件中可查看）</p>
<p>2、APPSECRET：公众帐号secert（仅JSAPI支付的时候需要配置， 登录公众平台，进入开发者中心可设置）， 请妥善保管， 避免密钥泄露</p>
<p>获取地址：<a href="https://mp.weixin.qq.com/advanced/advanced?action=dev&amp;t=advanced/dev&amp;token=2005451881&amp;lang=zh_CN" target="_blank">https://mp.weixin.qq.com/advanced/advanced?action=dev&amp;t=advanced/dev&amp;token=2005451881&amp;lang=zh_CN</a></p>
<p>&nbsp;</p>
<p>二、获取 MerchantId (MCHID)、KEY (商户支付密钥)</p>
<p>1、MCHID：商户号（必须配置，开户邮件中可查看）</p>
<p>2、KEY：商户支付密钥，参考开户邮件设置（必须配置，登录商户平台自行设置）, 请妥善保管， 避免密钥泄露</p>
<p>设置地址：<a href="https://pay.weixin.qq.com/index.php/account/api_cert" target="_blank">https://pay.weixin.qq.com/index.php/account/api_cert</a></p>
<p>&nbsp;</p>
<p>三、官网下载SDK文件</p>
<p><a href="https://pay.weixin.qq.com/wiki/doc/api/download/WxpayAPI_php.zip" target="_blank">https://pay.weixin.qq.com/wiki/doc/api/download/WxpayAPI_php.zip</a></p>
<p>&nbsp;</p>
<p>四、解压到网站根目录</p>
<p>1、修改lib/WxPay.Config.php为自己申请的商户号的信息（配置详见说明）</p>
<p>&nbsp;</p>
<p>五、下载证书替换cert下的文件</p>
<p>证书存放路径，证书可以登录商户平台<a href="https://pay.weixin.qq.com/index.php/account/api_cert" target="_blank">https://pay.weixin.qq.com/index.php/account/api_cert</a>下载</p>
<p>注意:</p>
<p>1、证书文件不能放在web服务器虚拟目录，应放在有访问权限控制的目录中，防止被他人下载；</p>
<p>2、建议将证书文件名改为复杂且不容易猜测的文件名；</p>
<p>3、商户服务器要做好病毒和木马防护工作，不被非法侵入者窃取证书文件。</p>
<p>&nbsp;</p>
<p>六、根据需求删改成适合的代码，完成。</p>
<p>&nbsp;</p>
