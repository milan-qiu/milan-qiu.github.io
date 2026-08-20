---
title: "03、Vue基础详解二"
date: "2020-04-08 15:26:00"
updated: "2020-04-08 17:47:00"
tags:
categories:
description: >-
  表单控件的绑定（v-model的双向绑定） text类型 //视图模板 <div> <h3>text</h3> <input type="text" v-model="text"> <p>{{text}}</p> </div> //data函数 data(){ return{ text:'' } }
---

<h2>表单控件的绑定（v-model的双向绑定）</h2>
<h3>text类型</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板</span>
&lt;div&gt;
    &lt;h3&gt;text&lt;/h3&gt;
    &lt;input type="text" v-model="text"&gt;
    &lt;p&gt;{{text}}&lt;/p&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data函数</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        text:</span>''<span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>radio类型</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板</span>
&lt;div&gt;
    &lt;h3&gt;radio&lt;/h3&gt;
    &lt;input type="radio" name="sex" value="male" v-model="radio" id="1"&gt; &lt;label <span style="color: #0000ff;">for</span>="1"&gt;Male&lt;/label&gt;&lt;br&gt;
    &lt;input type="radio" name="sex" value="female" v-model="radio" id="2"&gt;&lt;label <span style="color: #0000ff;">for</span>="2"&gt;Female&lt;/label&gt;&lt;br&gt;
    &lt;p&gt;{{radio}}&lt;/p&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data函数</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        radio:</span>''<span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>checkbox类型</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板</span>
&lt;div&gt;
    &lt;h3&gt;checkbox&lt;/h3&gt;
    &lt;input type="checkbox" name="aihao" value="打篮球" v-model="checkbox"&gt;打篮球&lt;br&gt;
    &lt;input type="checkbox" name="aihao" value="打" v-model="checkbox"&gt;打&lt;br&gt;
    &lt;input type="checkbox" name="aihao" value="篮" v-model="checkbox"&gt;篮&lt;br&gt;
    &lt;input type="checkbox" name="aihao" value="球" v-model="checkbox"&gt;球&lt;br&gt;
    &lt;p&gt;{{checkbox}}&lt;/p&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data函数</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        checkbox:[]
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>select类型</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板</span>
&lt;div&gt;
    &lt;h3&gt;select&lt;/h3&gt;
    &lt;select v-model="select"&gt;
        &lt;option disabled value=""&gt;请选择&lt;/option&gt;
        &lt;option&gt;A&lt;/option&gt;
        &lt;option&gt;B&lt;/option&gt;
        &lt;option&gt;C&lt;/option&gt;
    &lt;/select&gt;
    &lt;p&gt;{{ select }}&lt;/p&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data函数</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        checkbox:[]
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>表单提交</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板</span>
&lt;button v-on:click="submit"&gt;表单提交按钮&lt;/button&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">methods函数</span>
<span style="color: #000000;">methods:{
    submit(){
        </span><span style="color: #0000ff;">var</span> shujv =<span style="color: #000000;"> {
        radio:</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.radio,
        checkbox:</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.checkbox,
        select:</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.select
        };
    console.log(shujv);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>状态管理（vuex）</h2>
<h3>安装</h3>
<p>进入项目目录进行安装（可换cnpm）</p>
<div class="cnblogs_code">
<pre>npm install vuex --save</pre>
</div>
<p>&nbsp;</p>
<p>在src -&gt; main.js 引入</p>
<div class="cnblogs_code">
<pre>import store from './store'</pre>
</div>
<p>&nbsp;</p>
<p>并在new Vue代码段里，router下面使用store</p>
<div class="cnblogs_code">
<pre>router,<br />store,</pre>
</div>
<p>&nbsp;</p>
<p>在src目录下创建store文件夹</p>
<p>在store下创建index.js，并在里面写</p>
<div class="cnblogs_code">
<pre>import Vue from 'vue'<span style="color: #000000;">
import Vuex from </span>'vuex'<span style="color: #000000;">

Vue.use(Vuex)

export </span><span style="color: #0000ff;">default</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Vuex.Store({
    state: {
        count: </span>0<span style="color: #000000;">,
        num: </span>1<span style="color: #000000;">
    },
    mutations: {
        increment (state, num) {
          state.count</span>++<span style="color: #000000;">
          state.num </span>=<span style="color: #000000;"> num;
        }
    },
    actions: {
        inc ({ commit }, obj) {
              commit(</span>'increment'<span style="color: #000000;">, obj)
        }
    }
})</span></pre>
</div>
<p>&nbsp;</p>
<h3>获取数据</h3>
<p>//获取 store下 -&gt; index.js 里的全局数据</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">任何页面都可以进行获取</span>

<span style="color: #008000;">//</span><span style="color: #008000;">视图</span>
&lt;div&gt;
    &lt;div&gt;{{bbc}}&lt;/div&gt;
    &lt;button @click="qq"&gt;获取vuex全局数据&lt;/button&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        bbc:</span>'默认信息'<span style="color: #000000;">,
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">methods</span>
<span style="color: #000000;">methods:{
    qq(){
        </span><span style="color: #0000ff;">this</span>.bbc = <span style="color: #0000ff;">this</span><span style="color: #000000;">.$store.state.count;
        </span><span style="color: #008000;">//</span><span style="color: #008000;">获取store下，state对象，count属性的值</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>修改数据</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">methods</span>
<span style="color: #000000;">methods:{
    qq(){
        </span><span style="color: #008000;">//</span><span style="color: #008000;">修改数据</span>
        <span style="color: #0000ff;">this</span>.$store.dispatch('inc',2342<span style="color: #000000;">);
        </span><span style="color: #008000;">//</span><span style="color: #008000;">原理：</span>
        <span style="color: #008000;">//</span><span style="color: #008000;">调用store下的inc函数，并把2342的参数传过去</span>
        <span style="color: #008000;">//</span><span style="color: #008000;">通过inc修改state下的值</span>
        alert(<span style="color: #0000ff;">this</span><span style="color: #000000;">.bbc);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>slot插槽</h2>
<p>components下新建组件，plu.vue</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">template</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>插槽顶部<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">slot</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">slot</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>插槽末尾<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">slot </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="mowei"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">slot</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">template</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>正常调用插件</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">调用页：正常引入</span>
import sslot from '@/components/plu.vue'

<span style="color: #008000;">//</span><span style="color: #008000;">调用页：正常注册</span>
<span style="color: #000000;">components:{
    sslot
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">调用页：正常调用</span>
&lt;div&gt;
    &lt;sslot&gt;
    &lt;/sslot&gt;
&lt;/div&gt;</pre>
</div>
<p>&nbsp;</p>
<p>按照slot的name及默认值插入</p>
<div class="cnblogs_code">
<pre>&lt;sslot&gt;
    &lt;slot&gt;
        <span style="color: #008000;">//</span><span style="color: #008000;">&lt;!-- components组件页无论有多少slot标签，调用页只能有一个slot标签--&gt;</span>
        &lt;span v-bind:style="{color:'red'}"&gt;这是在调用插件的页面写的，默认插入到没有name值得slot里面&lt;/span&gt;<br />
        &lt;span slot="mowei" v-bind:style="{color:'orange'}"&gt;这里slot="mowei"，表示插入到name="mowei"的slot插槽里面&lt;/span&gt;
        <span style="color: #008000;">//</span><span style="color: #008000;">&lt;!-- ，里面内容以slot='xxx'的形式，分类插入到组件页slot的name='xxx'里面  --&gt;</span>
    &lt;/slot&gt;
&lt;/sslot&gt;</pre>
</div>
<p>&nbsp;</p>
<h2>vue-resource请求</h2>
<p>//该插件提供了使用XMLHttpRequest或JSONP 进行Web请求和处理响应的服务。</p>
<p>具体使用：<a href="https://github.com/pagekit/vue-resource">https://github.com/pagekit/vue-resource</a></p>
<h3>安装</h3>
<p>1、进入项目目录，开控制台下载（适当换成cnpm）</p>
<div class="cnblogs_code">
<pre>npm install vue-resource --save</pre>
</div>
<p>&nbsp;</p>
<p>2、src下main.js配置</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">引入</span>
import VueResource from 'vue-resource'
<span style="color: #008000;">//</span><span style="color: #008000;">全局使用</span>
Vue.use(VueResource);</pre>
</div>
<p>&nbsp;</p>
<h3>使用</h3>
<p>//在生命周期函数mounted下，进行使用</p>
<p>GET</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">get请求</span>
<span style="color: #0000ff;">this</span>.$http.get('/xxurl.php').then(response =&gt; {     <span style="color: #008000;">//</span><span style="color: #008000;"> /xxurl.php表示请求的url地址</span>
    console.log(response.body);     <span style="color: #008000;">//</span><span style="color: #008000;">response.body表示返回的数据</span>
}, response =&gt;<span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">错误回调</span>
});</pre>
</div>
<p>&nbsp;</p>
<p>POST</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">post请求</span>
<span style="color: #0000ff;">this</span>.$http.post('/someUrl', {     <span style="color: #008000;">//</span><span style="color: #008000;"> /xxurl.php表示请求的url地址</span>
    foo: 'bar'        <span style="color: #008000;">//</span><span style="color: #008000;">这里是参数传递</span>
}).then(response =&gt;<span style="color: #000000;"> {
    console.log(response.body);      </span><span style="color: #008000;">//</span><span style="color: #008000;">response.body表示返回的数据</span>
}, response =&gt;<span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">错误回调</span>
});</pre>
</div>
<p>&nbsp;</p>
<p>GET（带参数）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">get请求（带参数）</span>
<span style="color: #0000ff;">this</span>.$http.get('/someUrl'<span style="color: #000000;">, {
    params: {     </span><span style="color: #008000;">//</span><span style="color: #008000;">params为发送的参数对象</span>
        foo: 'bar'<span style="color: #000000;">
    },
    headers: {     </span><span style="color: #008000;">//</span><span style="color: #008000;">设置请求头</span>
        'X-Custom': '...'<span style="color: #000000;">
    }
}).then(response </span>=&gt;<span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">成功回调</span>
}, response =&gt;<span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">错误回调</span>
});</pre>
</div>
<p>&nbsp;</p>
<h2>移动组件库（Mint Ui）</h2>
<p>安装（适当用cnpm）</p>
<div class="cnblogs_code">
<pre>npm install mint-ui --save</pre>
</div>
<p>引入插件：src下main.js</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">引用</span>
import MintUi from 'mint-ui'
<span style="color: #008000;">//</span><span style="color: #008000;">引入css文件</span>
import 'mint-ui/lib/style.css'
<span style="color: #008000;">//</span><span style="color: #008000;">全局使用</span>
Vue.use(MintUi);</pre>
</div>
<p>&nbsp;</p>
<h3>使用</h3>
<p>更多使用详情：<a href="http://mint-ui.github.io/docs/#/zh-cn">http://mint-ui.github.io/docs/#/zh-cn</a></p>
<h3>Toast</h3>
<p>若要使用Toast，调用页script引入</p>
<div class="cnblogs_code">
<pre>import { Toast } from 'mint-ui';</pre>
</div>
<p>mounted函数使用</p>
<div class="cnblogs_code">
<pre>Toast('提示信息'<span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">或</span>
<span style="color: #000000;">Toast({
  message: </span>'提示'<span style="color: #000000;">,
  position: </span>'bottom'<span style="color: #000000;">,
  duration: </span>5000<span style="color: #000000;">
});</span></pre>
</div>
<h3>&nbsp;Tabbar</h3>
<p>&nbsp;若要使用Tabbar，调用页script引入</p>
<div class="cnblogs_code">
<pre>  import Vue from 'vue'<span style="color: #000000;">
  import { Tabbar, TabItem } from </span>'mint-ui'<span style="color: #000000;">;
  Vue.component(Tabbar.name, Tabbar);
  Vue.component(TabItem.name, TabItem);</span></pre>
</div>
<p>视图模板直接使用</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">mt-tabbar</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">mt-tab-item </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="外卖"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">img </span><span style="color: #ff0000;">slot</span><span style="color: #0000ff;">="icon"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../assets/100x100.png"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
          外卖
        </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">mt-tab-item</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">mt-tab-item </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="订单"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">img </span><span style="color: #ff0000;">slot</span><span style="color: #0000ff;">="icon"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../assets/100x100.png"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
          订单
        </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">mt-tab-item</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">mt-tab-item </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="发现"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">img </span><span style="color: #ff0000;">slot</span><span style="color: #0000ff;">="icon"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../assets/100x100.png"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
          发现
        </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">mt-tab-item</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">mt-tab-item </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="我的"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">img </span><span style="color: #ff0000;">slot</span><span style="color: #0000ff;">="icon"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../assets/100x100.png"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
          我的
        </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">mt-tab-item</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">mt-tabbar</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
