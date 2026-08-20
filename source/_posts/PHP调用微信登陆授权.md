---
title: "PHP调用微信登陆授权"
date: "2020-06-17 14:19:00"
tags:
categories:
description: >-
  一、配置公众号的appid、appsecret等信息 二、配置成功后返回的url 三、在返回的页面接收参数，执行相关操作 <?php /** * 获取微信用户信息 */ class GetWxUser{ private $appid = 'appidddd'; private $appsecret
---

<p>一、配置公众号的appid、appsecret等信息</p>
<p>&nbsp;</p>
<p>二、配置成功后返回的url</p>
<p>&nbsp;</p>
<p>三、在返回的页面接收参数，执行相关操作</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php
</span><span style="color: #008000;">/*</span><span style="color: #008000;">*
 * 获取微信用户信息
 </span><span style="color: #008000;">*/</span>

<span style="color: #0000ff;">class</span><span style="color: #000000;"> GetWxUser{    
    </span><span style="color: #0000ff;">private</span> <span style="color: #800080;">$appid</span> = 'appidddd'<span style="color: #000000;">;
    </span><span style="color: #0000ff;">private</span> <span style="color: #800080;">$appsecret</span> = 'appsecrettttt'<span style="color: #000000;">;
   </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
    * 1、获取微信用户信息，判断有没有code，有使用code换取access_token，没有去获取code。
    * @return array 微信用户信息数组
    </span><span style="color: #008000;">*/</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">function</span><span style="color: #000000;"> get_user(){
        </span><span style="color: #0000ff;">if</span> (!<span style="color: #0000ff;">isset</span>(<span style="color: #800080;">$_GET</span>['code'])){<span style="color: #008000;">//</span><span style="color: #008000;">没有code，去微信接口获取code码</span>
            <span style="color: #800080;">$callback</span> =  <span style="color: #800080;">$_SERVER</span>["REQUEST_SCHEME"]."://".<span style="color: #800080;">$_SERVER</span>['HTTP_HOST'].<span style="color: #800080;">$_SERVER</span>['PHP_SELF']."?url=".<span style="color: #800080;">$_GET</span>["url"];<span style="color: #008000;">//</span><span style="color: #008000;">微信服务器回调url，这里是本页url</span>
            <span style="color: #800080;">$this</span>-&gt;get_code(<span style="color: #800080;">$callback</span><span style="color: #000000;">);
        } </span><span style="color: #0000ff;">else</span> {<span style="color: #008000;">//</span><span style="color: #008000;">获取code后跳转回来到这里了</span>
            <span style="color: #800080;">$code</span> = <span style="color: #800080;">$_GET</span>['code'<span style="color: #000000;">];
            </span><span style="color: #800080;">$data</span> = <span style="color: #800080;">$this</span>-&gt;get_access_token(<span style="color: #800080;">$code</span>);<span style="color: #008000;">//</span><span style="color: #008000;">获取网页授权access_token和用户openid</span>
            <span style="color: #800080;">$data_all</span> = <span style="color: #800080;">$this</span>-&gt;get_user_info(<span style="color: #800080;">$data</span>['access_token'],<span style="color: #800080;">$data</span>['openid'],<span style="color: #800080;">$_GET</span>["url"]);<span style="color: #008000;">//</span><span style="color: #008000;">获取微信用户信息</span>
            <span style="color: #0000ff;">return</span> <span style="color: #800080;">$data_all</span><span style="color: #000000;">;
        }
    }
   </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
    * 2、用户授权并获取code
    * @param string $callback 微信服务器回调链接url
    </span><span style="color: #008000;">*/</span>
    <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">function</span> get_code(<span style="color: #800080;">$callback</span><span style="color: #000000;">){
        </span><span style="color: #800080;">$appid</span> = <span style="color: #800080;">$this</span>-&gt;<span style="color: #000000;">appid;
        </span><span style="color: #800080;">$scope</span> = 'snsapi_userinfo'<span style="color: #000000;">;
        </span><span style="color: #800080;">$state</span> = <span style="color: #008080;">md5</span>(<span style="color: #008080;">uniqid</span>(<span style="color: #008080;">rand</span>(), <span style="color: #0000ff;">TRUE</span>));<span style="color: #008000;">//</span><span style="color: #008000;">唯一ID标识符绝对不会重复</span>
        <span style="color: #800080;">$url</span> = 'https://open.weixin.qq.com/connect/oauth2/authorize?appid=' . <span style="color: #800080;">$appid</span> . '&amp;redirect_uri='.<span style="color: #008080;">urlencode</span>(<span style="color: #800080;">$callback</span>).'&amp;response_type=code&amp;scope=' . <span style="color: #800080;">$scope</span> . '&amp;state=' . <span style="color: #800080;">$state</span> . '#wechat_redirect'<span style="color: #000000;">;
        </span><span style="color: #008080;">header</span>("Location:<span style="color: #800080;">$url</span>"<span style="color: #000000;">);
    }    
   </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
    * 3、使用code换取access_token
    * @param string 用于换取access_token的code，微信提供
    * @return array access_token和用户openid数组
    </span><span style="color: #008000;">*/</span>
    <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">function</span> get_access_token(<span style="color: #800080;">$code</span><span style="color: #000000;">){
        </span><span style="color: #800080;">$appid</span> = <span style="color: #800080;">$this</span>-&gt;<span style="color: #000000;">appid;
        </span><span style="color: #800080;">$appsecret</span> = <span style="color: #800080;">$this</span>-&gt;<span style="color: #000000;">appsecret;    
        </span><span style="color: #800080;">$url</span> = 'https://api.weixin.qq.com/sns/oauth2/access_token?appid=' . <span style="color: #800080;">$appid</span> . '&amp;secret=' . <span style="color: #800080;">$appsecret</span> . '&amp;code=' . <span style="color: #800080;">$code</span> . '&amp;grant_type=authorization_code'<span style="color: #000000;">;
        </span><span style="color: #800080;">$user</span> = json_decode(<span style="color: #008080;">file_get_contents</span>(<span style="color: #800080;">$url</span><span style="color: #000000;">));
        </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">isset</span>(<span style="color: #800080;">$user</span>-&gt;<span style="color: #000000;">errcode)) {
               </span><span style="color: #0000ff;">echo</span> 'error:' . <span style="color: #800080;">$user</span>-&gt;errcode.'&lt;hr&gt;msg  :' . <span style="color: #800080;">$user</span>-&gt;<span style="color: #000000;">errmsg;
              </span><span style="color: #0000ff;">exit</span><span style="color: #000000;">;
        }
        </span><span style="color: #800080;">$data</span> = json_decode(json_encode(<span style="color: #800080;">$user</span>),<span style="color: #0000ff;">true</span>);<span style="color: #008000;">//</span><span style="color: #008000;">返回的json数组转换成array数组</span>
        <span style="color: #0000ff;">return</span> <span style="color: #800080;">$data</span><span style="color: #000000;">;
    }    
   </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
    * 4、使用access_token获取用户信息
    * @param string access_token
    * @param string 用户的openid
    * @return array 用户信息数组
    </span><span style="color: #008000;">*/</span>
    <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">function</span> get_user_info(<span style="color: #800080;">$access_token</span>,<span style="color: #800080;">$openid</span>,<span style="color: #800080;">$pth</span><span style="color: #000000;">){
        </span><span style="color: #800080;">$url</span> = 'https://api.weixin.qq.com/sns/userinfo?access_token=' . <span style="color: #800080;">$access_token</span> . '&amp;openid=' . <span style="color: #800080;">$openid</span> . '&amp;lang=zh_CN'<span style="color: #000000;">;
        </span><span style="color: #800080;">$user</span> = <span style="color: #008080;">file_get_contents</span>(<span style="color: #800080;">$url</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">isset</span>(<span style="color: #800080;">$user</span>-&gt;<span style="color: #000000;">errcode)) {
               </span><span style="color: #0000ff;">echo</span> 'error:' . <span style="color: #800080;">$user</span>-&gt;errcode.'&lt;hr&gt;msg  :' . <span style="color: #800080;">$user</span>-&gt;<span style="color: #000000;">errmsg;
              </span><span style="color: #0000ff;">exit</span><span style="color: #000000;">;
        }
          </span><span style="color: #800080;">$s</span>=<span style="color: #800080;">$pth</span>==''?"?":"&amp;"<span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var_dump( $_SERVER);</span>
      <span style="color: #0000ff;">echo</span> <span style="color: #800080;">$_SERVER</span>["REQUEST_SCHEME"]."://".<span style="color: #800080;">$_SERVER</span>['HTTP_HOST']."/".<span style="color: #800080;">$pth</span>.<span style="color: #800080;">$s</span>."val=".<span style="color: #800080;">$user</span><span style="color: #000000;">;
     </span><span style="color: #008080;">header</span>("Location:". <span style="color: #800080;">$_SERVER</span>["REQUEST_SCHEME"]."://".<span style="color: #800080;">$_SERVER</span>['HTTP_HOST']."/quest/Assessment/index.php 这里配置返回地址".<span style="color: #800080;">$pth</span>.<span style="color: #800080;">$s</span>."val=".<span style="color: #008080;">urlencode</span>(<span style="color: #800080;">$user</span><span style="color: #000000;">));
        </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">$user</span><span style="color: #000000;">;
    }    
}
</span><span style="color: #800080;">$g</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> GetWxUser();
</span><span style="color: #800080;">$g</span>-&gt;<span style="color: #000000;">get_user();
</span>?&gt;</pre>
</div>
<p>&nbsp;</p>
