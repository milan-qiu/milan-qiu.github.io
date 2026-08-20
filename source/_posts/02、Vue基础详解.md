---
title: "02、Vue基础详解"
date: "2020-04-05 20:13:00"
updated: "2020-04-07 16:07:00"
tags:
categories:
description: >-
  环境准备 1、安装node.js，为了使用npm 2、装完后，cmd进入控制台，查看node版本号node -v，查看npm版本号npm -v 3、查看path环境变量，cmd进入控制台，输入path查看是否有node字样，没问题进入下一步。 4、安装git，为了快捷地开发 5、装完之后，在需要开发
---

<h2>环境准备</h2>
<p>1、安装node.js，为了使用npm</p>
<p>2、装完后，cmd进入控制台，查看node版本号node -v，查看npm版本号npm -v</p>
<p>3、查看path环境变量，cmd进入控制台，输入path查看是否有node字样，没问题进入下一步。</p>
<p>&nbsp;</p>
<p>4、安装git，为了快捷地开发</p>
<p>5、装完之后，在需要开发的文件夹里面右击，选择Git Bash Here</p>
<p>&nbsp;</p>
<p>6、由于npm源在国外速度慢，可以选择换源，或者使用淘宝镜像工具</p>
<p>7、安装淘宝npm镜像，可以使用cnpm，代替npm</p>
<div class="cnblogs_code">
<pre>npm install -g cnpm --registry=https:<span style="color: #008000;">//</span><span style="color: #008000;">registry.npm.taobao.org</span></pre>
</div>
<p>&nbsp;</p>
<p>8、安装vue（其中的npm命令可以适当换成cnpm）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">全局安装vue-cli</span>
npm install --global vue-<span style="color: #000000;">cli

</span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个基于webpack模板的新项目</span>
vue init webpack my-<span style="color: #000000;">project
</span><span style="color: #008000;">//</span><span style="color: #008000;">其他选项都可以直接回车或输入N回车，在vue-router的时候，输入Y回车<br />//当看见All packages installed，就完成了<br /></span>

<span style="color: #008000;">//</span><span style="color: #008000;">安装依赖包</span>
cd my-<span style="color: #000000;">project
npm install
npm run dev</span></pre>
</div>
<p>&nbsp;9、项目进行中时不要关闭git，若关闭了重新打开：cd my-project&nbsp; ,npm run dev 即可</p>
<p>&nbsp;</p>
<h2>项目的创建</h2>
<p>&nbsp;1、在src目录下面创建自己的项目文件夹，如bb</p>
<p>&nbsp;2、在该项目下面创建视图文件，xxx.vue</p>
<div class="cnblogs_code">
<pre>&lt;template&gt;
　　&lt;p&gt;Hello World&lt;/p&gt;
&lt;/template&gt;</pre>
</div>
<p>&nbsp;3、设置路由，src目录下的router下的index.js，如：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">import HelloWorld from </span>'@/components/HelloWorld' <span style="color: #008000;">/*</span><span style="color: #008000;">当前@表示src目录</span><span style="color: #008000;">*/</span><span style="color: #000000;">
import xiangmu from </span>'@/xiangmu/index.vue' <span style="color: #008000;">/*</span><span style="color: #008000;">第二种引入方式</span><span style="color: #008000;">*/</span><span style="color: #000000;">

export </span><span style="color: #0000ff;">default</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Router({
  routes: [{
      path: </span>'/', <span style="color: #008000;">//</span><span style="color: #008000;">当地址栏输入/的时候，找到下面component的地址</span>
      name: 'HelloWorld', <span style="color: #008000;">//</span><span style="color: #008000;">按照需求给这个路由命名</span>
      component: HelloWorld <span style="color: #008000;">//</span><span style="color: #008000;">地址栏</span>
    }, <span style="color: #008000;">//</span><span style="color: #008000;">记得两个路由之间要加上逗号</span>
<span style="color: #000000;">    {
      path: </span>'/xiangmu'<span style="color: #000000;">,
      name: </span>'xiangmu'<span style="color: #000000;">,
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> component: require('@/xiangmu/index.vue') //第一种引入方式，这种方式有些版本不支持</span>
      component: xiangmu <span style="color: #008000;">//</span><span style="color: #008000;">第二种方式，全通用</span>
<span style="color: #000000;">    }
  ]
})</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;4、去掉默认大logo，src目录下App.vue，删除开头的的&lt;img src="./assets/logo.png"&gt;标签，完成</p>
<p>&nbsp;5、浏览器访问&nbsp; http://localhost:8080/#/&nbsp; 到达首页</p>
<p>&nbsp;&nbsp;</p>
<h2>生命周期</h2>
<p>生命周期图片：<a href="https://cn.vuejs.org/images/lifecycle.png">https://cn.vuejs.org/images/lifecycle.png</a></p>
<p>组件生成的时候就会自动调用生命周期函数，具体生命周期的实现如：</p>
<div class="cnblogs_code">
<pre>&lt;script&gt;<span style="color: #000000;">
    export </span><span style="color: #0000ff;">default</span><span style="color: #000000;">{
        data(){   </span><span style="color: #008000;">//</span><span style="color: #008000;">每个组件都会有data这个函数</span>
            <span style="color: #0000ff;">return</span><span style="color: #000000;">{}
        },  </span><span style="color: #008000;">//</span><span style="color: #008000;">两函数之间要用逗号隔开</span>
<span style="color: #000000;">
        beforeCreate(){
            console.log(</span>'beforeCreate 创建之前'<span style="color: #000000;">);
        },
        created(){
            console.log(</span>'created 已经创建'<span style="color: #000000;">);
        },
        beforeMount(){
            console.log(</span>'beforeMount 挂载之前'<span style="color: #000000;">);
        },
        mounted(){
            console.log(</span>'mounted 已经挂载'<span style="color: #000000;">);
        },
                
        </span><span style="color: #008000;">//</span><span style="color: #008000;">生命周期函数监听到才触发</span>
<span style="color: #000000;">
        beforeUpdate(){
            console.log(</span>'beforeUpdate 更新之前'<span style="color: #000000;">);
        },
        updated(){
            console.log(</span>'updated 已经更新'<span style="color: #000000;">);
        },
        beforeDestroy(){
            console.log(</span>'beforeDestroy 销毁之前'<span style="color: #000000;">);
        },
        destroyed(){
            console.log(</span>'destroyed 已经销毁'<span style="color: #000000;">);
        }
    }
</span>&lt;/script&gt;</pre>
</div>
<p>&nbsp;</p>
<h2>选项数据</h2>
<h3>data</h3>
<div class="cnblogs_code">
<pre>  export <span style="color: #0000ff;">default</span><span style="color: #000000;"> {
    data() {
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        bb: </span>'hello', <span style="color: #008000;">//</span><span style="color: #008000;">两个变量之间用逗号分隔</span>
        cc: 'how are you' <span style="color: #008000;">//</span><span style="color: #008000;">这里定义的是全局变量，视图模板可以用，后续函数也可以用</span>
<span style="color: #000000;">      }
    },<br />　　//code...
  }</span></pre>
</div>
<p>模板调用</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">template</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;　　&lt;!-- 如需调用不多个选项数据，那必须在该div里面 --&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>{{bb}}<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span> <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">模板调用只需要 {{变量名}} 即可</span><span style="color: #008000;">--&gt;<br />　　&lt;!-- code... --&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">template</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<h2>computed</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">//接着上面的export default 里面定义<br />computed: { </span><span style="color: #008000;">//</span><span style="color: #008000;">computed是一个对象，里面可以定义各种函数</span>
<span style="color: #000000;">　　hi() {
</span><span style="color: #0000ff;">　　　　return</span> <span style="color: #0000ff;">this</span>.bb + <span style="color: #0000ff;">this</span>.cc; <span style="color: #008000;">//</span><span style="color: #008000;">调用data里面的变量 = this.变量名</span>
<span style="color: #000000;">　　}
}, </span></pre>
</div>
<p>模板调用</p>
<div class="cnblogs_code">
<pre>//接着在模板{{bb}}后面写<br />&lt;div&gt;{{hi}}&lt;/div&gt;</pre>
</div>
<p>&nbsp;</p>
<h2>methods</h2>
<div class="cnblogs_code">
<pre>methods:{  <span style="color: #008000;">//</span><span style="color: #008000;">methods对象，里面定义各种行为性的函数</span>
<span style="color: #000000;">　　hello(){
　　　　alert(</span>"hello"<span style="color: #000000;">);
　　}
}</span></pre>
</div>
<p>模板调用</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">接着在模板{{hi}}后面写</span>
&lt;div @click="hello()"&gt;打招呼&lt;/div&gt;  //用@click给该div绑定点击事件<br />//函数不需要传参时，后面()可写可不写</pre>
</div>
<p>&nbsp;</p>
<h2>模板语法&nbsp;</h2>
<h3>data语法</h3>
<p>//在模板输出data属性（选项数据说过）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        bb: </span>'Hello!'<span style="color: #000000;">
    }
}    
</span><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;{{bb}}&lt;/div&gt;</pre>
</div>
<p>&nbsp;</p>
<h3>嵌入js语法</h3>
<p>//在模板上面嵌入js</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        bb: </span>'Hello!  ', <span style="color: #008000;">//</span><span style="color: #008000;">两个变量之间用逗号分隔</span>
        cc: 'How are you?' <span style="color: #008000;">//</span><span style="color: #008000;">这里定义的是全局变量，视图模板可以用，后续函数也可以用</span>
<span style="color: #000000;">    }
}  
</span><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;{{bb + cc +bb}}&lt;/div&gt;  //js的字符串拼接 </pre>
</div>
<p>&nbsp;</p>
<h3>v-html</h3>
<p>//动态地嵌入html标签</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        dt:</span>"&lt;p&gt;html是动态的，更改data里面属性值，html就会变化&lt;/p&gt;"<span style="color: #000000;">
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-html="dt"&gt;&lt;/div&gt;    //将dt里面的html嵌入到这个div里面</pre>
</div>
<p>&nbsp;</p>
<h3>v-bind</h3>
<p>//动态的属性名</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        lei:</span>"nihao"<span style="color: #000000;">
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-bind:class="lei"&gt;&lt;/div&gt;    
<span style="color: #008000;">//</span><span style="color: #008000;">class = data里面lei的value 。</span><span style="color: #008000;">
//</span><span style="color: #008000;">更改lei的value，该div的class就会发生改变</span></pre>
</div>
<p>&nbsp;</p>
<h3>v-on</h3>
<p>//绑定事件函数</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">methods定义</span>
<span style="color: #000000;">methods:{
    say(h){
        alert(h);
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-on:click="say(hi)"&gt;点击触发函数&lt;/div&gt;    
<span style="color: #008000;">//</span><span style="color: #008000;">缩写形式：@click="say(hi)"</span></pre>
</div>
<p>&nbsp;</p>
<h3>过滤器</h3>
<p>//对模板中的变量进行过滤，通过过滤器，改变原来的输出</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        bb:</span>"你好！"<span style="color: #000000;">
    }
},
</span><span style="color: #008000;">//</span><span style="color: #008000;">filters定义，filters里面定义各种过滤器函数</span>
<span style="color: #000000;">methods:{
    say(h){
        alert(h</span>+<span style="color: #000000;">h);
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt; {{bb | say(bb)}} &lt;/div&gt;    //输出结果：你好！你好！
<span style="color: #008000;">//</span><span style="color: #008000;">没有过滤器的时候直接输出bb变量，通过say(bb)过滤器,输出了两个bb变量</span></pre>
</div>
<p>&nbsp;</p>
<h3>计算属性（computed）</h3>
<p>//模板与js分离（过多的嵌套js会导致模板页面维护成本变高）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">js分离：模板文件容易维护</span>

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        bb:</span>"Hello！"<span style="color: #000000;">
    }
},
</span><span style="color: #008000;">//</span><span style="color: #008000;">computed定义</span>
<span style="color: #000000;">computed: {
    fanzhuan(){
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span>.bb.split('').reverse().join(''<span style="color: #000000;">);
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt; {{bb}} &lt;/div&gt;</pre>
</div>
<p>&nbsp;</p>
<h2>class动态绑定</h2>
<h3>第一种方式</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-bind:class="{'inner':isinner,'active':isactive}"&gt;第一种&lt;/div&gt; 
&lt;!-- 用了引号的是class名，没用引号的是变量 --&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){<br />　　return{
     isinner:</span><span style="color: #0000ff;">true</span>,    <span style="color: #008000;">//</span><span style="color: #008000;">true表示该属性生效</span>
     isactive:<span style="color: #0000ff;">false</span>  <span style="color: #008000;">//</span><span style="color: #008000;">false表示该属性不生效<br />　　}<br /></span>}</pre>
</div>
<p>&nbsp;</p>
<h3>第二种方式（个人推荐）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div :class="classObject"&gt;第二种&lt;/div&gt;
&lt;!-- :class 是 v-bind:class 的缩写 --&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        isinner:</span><span style="color: #0000ff;">false</span>,    <span style="color: #008000;">//</span><span style="color: #008000;">false表示该属性不生效</span>
        isactive:<span style="color: #0000ff;">true</span>  <span style="color: #008000;">//</span><span style="color: #008000;">true表示该属性生效</span>
        <span style="color: #008000;">//</span><span style="color: #008000;">这里可以添加适当多的class</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>第三种</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div :class="[aclass,bclass]"&gt;第三种&lt;/div&gt;
&lt;!-- 这里aclass和bclass指的是data的变量 --&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        aclass:</span>'abc'<span style="color: #000000;">,
        bclass:</span>'def'<span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>style动态绑定</h2>
<p>//不推荐style嵌套在html中</p>
<h3>第一种</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-bind:style="{'color':color1,'background-color':color2}"&gt;style第一种&lt;/div&gt;
&lt;!-- 这里color1 和 color2指的是data的变量 --&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        color1:</span>'red',    <span style="color: #008000;">//</span><span style="color: #008000;">这里所有不加引号的都表示变量</span>
        color2:'orange'  <span style="color: #008000;">//</span><span style="color: #008000;">加了引号的才表示字符串</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>第二种</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-bind:style="styleObject"&gt;style第二种&lt;/div&gt;
&lt;!-- 所有样式都可以存储在styleObject里面 --&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        styleObject:{
            </span>'color':'yellow'<span style="color: #000000;">,
            </span>'background-color':'green'
            <span style="color: #008000;">/*</span><span style="color: #008000;">这里可以添加各种样式</span><span style="color: #008000;">*/</span><span style="color: #000000;">
       }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>第三种</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-bind:style="[ziti,beijing]"&gt;style第三种&lt;/div&gt;
&lt;!-- 数组里面的ziti和beijing都是对象，每个对象都可以有多种样式 --&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
       ziti:{ </span><span style="color: #008000;">//</span><span style="color: #008000;">这里可以添加多种样式</span>
         'color':'cyan'<span style="color: #000000;">
       },
       beijing:{ </span><span style="color: #008000;">//</span><span style="color: #008000;">这里可以添加多种样式</span>
         'background-color':'blue'<span style="color: #000000;">
       }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>条件渲染</h2>
<h3>v-if</h3>
<p>//当v-if的属性值为真就执行</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-<span style="color: #0000ff;">if</span>="bb"&gt;当bb为真，打印出if语句&lt;/div&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        bb:</span><span style="color: #0000ff;">true</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>v-if&nbsp; v-else</h3>
<p>//若v-if条件为假，则执行v-else的内容</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-<span style="color: #0000ff;">if</span>="bb === 'A'"&gt;选项A&lt;/div&gt;&lt;!-- 判断bb变量的值是否===A，是就执行 --&gt;
&lt;div v-<span style="color: #0000ff;">else</span>&gt;其他选项&lt;/div&gt;
&lt;!-- 注意v-else后面不需要属性值 --&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        bb:</span>'A'    <span style="color: #008000;">//</span><span style="color: #008000;">这里控制if和else哪个输出</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>v-if&nbsp; v-else-if&nbsp; v-else</h3>
<p>//若条件不等于v-if v-else-if，则输出v-else</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-<span style="color: #0000ff;">if</span>="dd==='D'"&gt;dd==='D'输出这项&lt;/div&gt;
&lt;div v-<span style="color: #0000ff;">else</span>-<span style="color: #0000ff;">if</span>="dd==='E'"&gt;dd==='E'输出这项&lt;/div&gt;
&lt;div v-<span style="color: #0000ff;">else</span>&gt;dd的变量非DE，输出这项&lt;/div&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        dd:</span>'E'    <span style="color: #008000;">//</span><span style="color: #008000;">这里控制输出语句</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<h3>&nbsp;v-show</h3>
<p>//跟v-if差不多一样，只要条件为真就输出</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div v-show="bb"&gt;当bb为真输出此语句&lt;/div&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        bb:</span><span style="color: #0000ff;">true</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>列表渲染</h2>
<h3>v-for循环输出数组</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
&lt;ul&gt;
    &lt;li v-<span style="color: #0000ff;">for</span>="child in parents"&gt;{{child}}&lt;/li&gt;
    &lt;!-- 其中parents为数组变量，child为数组中的每一项数据，child名字自定以 --&gt;
&lt;/ul&gt;
&lt;/div&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        parents:[</span>1,2,3,4,5]     <span style="color: #008000;">//</span><span style="color: #008000;">数组定义</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>v-for循环数组，带下标</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
&lt;ul&gt;
    &lt;li v-<span style="color: #0000ff;">for</span>="(child,index) in parents"&gt;{{child}}下标为{{index}}&lt;/li&gt;
    &lt;!-- 其中parents为数组变量，child为数组中的每一项数据，index为所对应的数组下标 --&gt;
&lt;/ul&gt;
&lt;/div&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        parents:[</span>1,2,3,4,5]     <span style="color: #008000;">//</span><span style="color: #008000;">数组定义</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>v-for循环输出对象</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
&lt;ul&gt;
      &lt;li v-<span style="color: #0000ff;">for</span>="(value,key) in obj"&gt;{{key}}:{{value}}&lt;/li&gt;
      &lt;!-- ()里面的值，第一个必须是属性值value，其次才是key，不然容易混乱 --&gt;
      &lt;!-- obj为对象变量--&gt;
&lt;/ul&gt;
&lt;/div&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
        obj:{
          </span>'name':'张三'<span style="color: #000000;">,
          </span>'age':'18岁'<span style="color: #000000;">,
          </span>'sex':'female'<span style="color: #000000;">,
          </span>'address':'beijing'<span style="color: #000000;">
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>事件处理器</h2>
<p>//v-on:click的缩写是@click</p>
<p>行内直接执行</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
    &lt;div&gt;
      &lt;p&gt;按钮被点击了{{a}}次&lt;/p&gt;
      &lt;button v-on:click="a+=1"&gt;计算点击次数&lt;/button&gt;
    &lt;/div&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
       a:</span>0<span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>行内调用函数（不传参）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
    &lt;div&gt;
      &lt;p&gt;按钮被点击了{{a}}次&lt;/p&gt;
      &lt;button v-on:click="count"&gt;计算点击次数&lt;/button&gt;
    &lt;/div&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data定义</span>
<span style="color: #000000;">data(){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
       a:</span>0<span style="color: #000000;">
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">methods定义</span>
<span style="color: #000000;">methods:{
    count(){
        </span><span style="color: #0000ff;">this</span>.a+=1<span style="color: #000000;">;
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>行内调用函数（传参）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
    &lt;div&gt;
      &lt;button v-on:click="hello('打招呼实参')"&gt;调用传参的函数&lt;/button&gt;
    &lt;/div&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">methods定义</span>
<span style="color: #000000;">methods:{
    hello(a){
        alert(a);
    }
}</span></pre>
</div>
<p>&nbsp;默认冒泡机制（不阻止）</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//点击会有两个弹框<br />//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
    &lt;div @click="hello('第二次冒泡')"&gt;
        &lt;button v-on:click="hello('第一次冒泡')"&gt;调用传参的函数&lt;/button&gt;
    &lt;/div&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">methods定义</span>
<span style="color: #000000;">methods:{
    hello(a){
        alert(a);
    }
}</span></pre>
</div>
<p>阻止冒泡</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//只会出现一个弹框<br />//</span><span style="color: #008000;">模板输出</span>
&lt;div&gt;
    &lt;div @click="hello('第二次冒泡')"&gt;
        &lt;button v-on:click="hello('第一次冒泡')"&gt;调用传参的函数&lt;/button&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">阻止冒泡只需在v-on:click或@click后面加上 .stop 即可</span>
    &lt;/div&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">methods定义</span>
<span style="color: #000000;">methods:{
    hello(a){
        alert(a);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>自定义组件</h2>
<h3>首先</h3>
<p>在src的components下面写好组件</p>
<div class="cnblogs_code">
<pre>&lt;template&gt;
   &lt;div&gt;{{time}}&lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;<span style="color: #000000;">
 export </span><span style="color: #0000ff;">default</span><span style="color: #000000;">{
   data(){
     </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
       time:</span>100<span style="color: #000000;">
     }
   },
   mounted(){  </span><span style="color: #008000;">//</span><span style="color: #008000;">组件被挂载之后执行</span>
   <span style="color: #0000ff;">var</span> t = <span style="color: #0000ff;">this</span><span style="color: #000000;">;
   </span><span style="color: #008000;">//</span><span style="color: #008000;">把整个data函数存储路径复制过来，这样修改time值才会改变</span>
   <span style="color: #008000;">//</span><span style="color: #008000;">原理是引用数据类型直接赋值的是路径，而不是数据本身，直接修改的话是修改源函数</span>
   <span style="color: #008000;">//</span><span style="color: #008000;">若直接把this.time复制过来的话，复制的是基本数据类型，更改基本数据类型的数据起不到页面数据更改的效果</span>
   setInterval(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
       t.time</span>--; <span style="color: #008000;">//</span><span style="color: #008000;">这样更改才会改变data里面的源数据</span>
     },1000<span style="color: #000000;">)
   }
 }
</span>&lt;/script&gt;</pre>
</div>
<h3><span style="font-size: 1.17em;">接着</span></h3>
<p>在需要组件的页面上</p>
<div class="cnblogs_code">
<pre>&lt;template&gt;
  &lt;div&gt;
    &lt;div&gt;引入components插件&lt;/div&gt;
    <span style="color: #008000;">//</span><span style="color: #008000;">&lt;!-- 第四步：在模板某个地方生成组件 --&gt;</span>
    &lt;daoji&gt; 若在第三步更换了名字，则标签就是该名字 &lt;/daoji&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">第一步：像写路由一样，把页面引进来</span>
import daoji from '@/components/daoji.vue'<span style="color: #000000;">

  export </span><span style="color: #0000ff;">default</span><span style="color: #000000;">{
    data(){
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;">{
      }
    },
    components:{  </span><span style="color: #008000;">//</span><span style="color: #008000;">第二步：把引进来的组件写进去才能生效</span>
      daoji   <span style="color: #008000;">//</span><span style="color: #008000;">第三步：可以更换名字，如：'aa':daoji，这样也能生效</span>
<span style="color: #000000;">    }
  }
</span>&lt;/script&gt;</pre>
</div>
<p>&nbsp;</p>
<h2>添加组件样式</h2>
<p>1、在调用组件的页面，传参到components组件页</p>
<div class="cnblogs_code">
<pre>&lt;jj col="red"&gt;这是生成组件的标签&lt;/jj&gt;
    <span style="color: #008000;">//</span><span style="color: #008000;">将col属性传入components页</span></pre>
</div>
<p>&nbsp;</p>
<p>2、在components组件页，script部分接收参数</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">这个对象定义在export default里面<br /></span>
props:{  <span style="color: #008000;">//</span><span style="color: #008000;">接收数据的对象</span>
    col:{    <span style="color: #008000;">//</span><span style="color: #008000;">发送过来的col，满足下面条件才生效</span>
        type:String,  <span style="color: #008000;">//</span><span style="color: #008000;">要求接收到的是字符串,String首字母一定要大写</span>
        <span style="color: #0000ff;">default</span>:'black'  <span style="color: #008000;">//</span><span style="color: #008000;">默认值，没接收到数据时用</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>3、在components组件页，template部分定义样式</p>
<div class="cnblogs_code">
<pre>&lt;template&gt;
   &lt;p :style="{color:col}"&gt;{{time}}&lt;/p&gt;
&lt;/template&gt;</pre>
</div>
<p>&nbsp;</p>
<h2>添加组件行为</h2>
<p>1、components组件页中，当倒计时结束时，触发函数end</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">if</span>(t.time == 0<span style="color: #000000;">){
t.$emit(</span>"end"); <span style="color: #008000;">//</span><span style="color: #008000;">当time=0时，触发end，end是自定义的名称</span>
<span style="color: #000000;">clearInterval(dd);
}</span></pre>
</div>
<p>2、在调用页中定义@end，并指定页面中触发的函数ending</p>
<div class="cnblogs_code">
<pre>&lt;jj @end="ending"&gt; 这是生成组件的标签 &lt;/jj&gt;</pre>
</div>
<p>3、同时在调用页中定义ending函数</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">methods:{
    ending(){
        alert(</span>"结束了"<span style="color: #000000;">);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>DOM操作</h2>
<p>首先在模板文件定义ref属性，如</p>
<div class="cnblogs_code">
<pre>&lt;div ref="hhead"&gt;&lt;/div&gt;   //ref属性值自定义</pre>
</div>
<p>接着在mounted下操作DOM</p>
<div class="cnblogs_code">
<pre>mounted(){  <span style="color: #008000;">//</span><span style="color: #008000;">在mounted下，所有的DOM都是真实DOM</span>
  <span style="color: #0000ff;">this</span>.$refs.hhead.innerText = '经过Dom操作出来的内容'<span style="color: #000000;">;
 </span><span style="color: #008000;">//</span><span style="color: #008000;">this . $refs . 模板ref属性值 . innerText等操作</span>
}</pre>
</div>
<p>&nbsp;</p>
<h2>&nbsp;过渡效果</h2>
<p>&nbsp;//没有过渡效果时，隐藏和出现都是一闪而过</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">template模板</span>
&lt;div id="demo"&gt;
    &lt;button v-on:click="show = !show"&gt;    <span style="color: #008000;">//</span><span style="color: #008000;">点击按钮实现show的真假转换</span>
<span style="color: #000000;">        Toggle
    </span>&lt;/button&gt;
    &lt;transition name="fade"&gt;    <span style="color: #008000;">//</span><span style="color: #008000;">vue框架的过渡标签，不定义样式不起效果</span>
        &lt;p v-<span style="color: #0000ff;">if</span>="show"&gt;hello&lt;/p&gt;    //通过获取show的真假，实现p标签是否输出
    &lt;/transition&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">data函数定义</span>
<span style="color: #000000;">data() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> {
        show: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>//添加过渡效果，实现淡入淡出</p>
<div class="cnblogs_code">
<pre>&lt;style&gt;
<span style="color: #008000;">/*</span><span style="color: #008000;">获取transition标签的name属性</span><span style="color: #008000;">*/</span><span style="color: #000000;">
.fade</span>-leave,.fade-enter-to{ <span style="color: #008000;">/*</span><span style="color: #008000;">一般默认opacity都是1，这项可省略</span><span style="color: #008000;">*/</span><span style="color: #000000;">
  opacity:</span>1<span style="color: #000000;">;
}
.fade</span>-leave-active,.fade-enter-<span style="color: #000000;">active{
  transition: opacity .5s;  </span><span style="color: #008000;">/*</span><span style="color: #008000;">过渡效果为opacity，在0.5秒内完成</span><span style="color: #008000;">*/</span><span style="color: #000000;">
}
.fade</span>-leave-to,.fade-<span style="color: #000000;">enter{
  opacity:</span>0<span style="color: #000000;">;
}
</span><span style="color: #008000;">/*</span><span style="color: #008000;">样式中.fade表示transition的name值</span><span style="color: #008000;">*/</span>
&lt;/style&gt;

<span style="color: #008000;">//</span><span style="color: #008000;">（淡入）隐藏效果opacity从1到0，分为三个状态呈现</span><span style="color: #008000;">
//</span><span style="color: #008000;">.fade-leave(1) -&gt; .fade-leave-active(.5) -&gt; .fade-leave-to(0)</span>

<span style="color: #008000;">//</span><span style="color: #008000;">（淡出）出现效果opacity从0到1，分为三个状态呈现</span><span style="color: #008000;">
//</span><span style="color: #008000;">.fade-enter(0) -&gt; .fade-enter-active(.5) -&gt; .fade-enter-to(1)</span></pre>
</div>
<p>&nbsp;</p>
<h2>路由跳转（vue-router）</h2>
<h3>模板直接跳转</h3>
<div class="cnblogs_code">
<pre>&lt;div&gt;
    &lt;router-link to="/liebiao"&gt;列表渲染（直接跳转）&lt;/router-link&gt;
    <span style="color: #008000;">//</span><span style="color: #008000;">&lt;!-- router-link相当于a标签，to相当于href，to的属性值为路由表的path --&gt;</span>
&lt;/div&gt;</pre>
</div>
<h3>模板带参数跳转（带params）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板（发送页）</span>
&lt;div&gt;
    &lt;router-link :to="{name:'tiaojian',params:{name:'zhangsan'}}"&gt;条件渲染（带参数跳转）&lt;/router-link&gt;
    <span style="color: #008000;">//</span><span style="color: #008000;">&lt;!-- :to表示v-bind:to，后面的参数可以直接用变量 --&gt;</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">&lt;!-- 跳转方式可以用name跳转（name:'tiaojian'），也可以用path跳转（path:'/tiaojian'）,参照router下的路由表 --&gt;</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">&lt;!-- params后面的参数是通过get的方式发送， --&gt;</span>
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">路由表</span>
<span style="color: #000000;">{
    path:</span>'/tiaojian/:name',      <span style="color: #008000;">//</span><span style="color: #008000;">:name表示：接收name属性 所对应的对象params，及后面的对象query，的所有内容</span>
    name:'tiaojian'<span style="color: #000000;">,
    component:tiaojian
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">mounted函数（接收页）</span>
<span style="color: #000000;">mounted(){
    alert(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.$route.params.name);
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 接收params数据用：this.$route.params.属性名</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>模板带参数跳转（带params &amp; query）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板（发送页）</span>
&lt;div&gt;
    &lt;router-link :to="{ name:'bangding',params:{name:'张三',address:'北京'},query:{age:18} }"&gt;<span style="color: #000000;">
    css与style绑定
    </span>&lt;/router-link&gt;
&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">路由表</span>
<span style="color: #000000;">{
    path: </span>'/bangding/:name',  <span style="color: #008000;">//</span><span style="color: #008000;">:name表示：接收name属性 所对应的对象params，及后面的对象query，的所有内容</span>
    name: 'bangding'<span style="color: #000000;">,
    component: bangding
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">mounted函数（接收页）</span>
<span style="color: #000000;">mounted(){
    alert(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.$route.query.age);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">接收query数据：this.$route.query.属性名</span>
}</pre>
</div>
<p>&nbsp;</p>
<h3>js直接跳转</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板（发送页）</span>
&lt;div @click="toUrl"&gt;组件(js直接跳)&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">methods（发送页）</span>
<span style="color: #000000;">methods:{
    toUrl(){
        </span><span style="color: #0000ff;">this</span>.$router.push({ path:'/zujian'<span style="color: #000000;"> });
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>js跳转（带params）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板（发送页）</span>
&lt;div v-on:click="url"&gt;事件处理（js跳，带params）&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">methods（发送页）</span>
<span style="color: #000000;">methods:{
    url(){
      </span><span style="color: #0000ff;">this</span>.$router.push({name:'shijian',params:{fa:'带params参数跳'<span style="color: #000000;">}});
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">接收页的路由表</span><span style="color: #008000;">
//</span><span style="color: #008000;">根据实际情况选择写或不写</span>

<span style="color: #008000;">//</span><span style="color: #008000;">mounted函数（接收页）</span>
<span style="color: #000000;">mounted(){
    alert(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.$route.params.fa);
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>js跳转（带params &amp; query）</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">视图模板（发送页）</span>
&lt;div @click="uurl"&gt;项目（js跳，带params &amp; query）&lt;/div&gt;
<span style="color: #008000;">//</span><span style="color: #008000;">methods（发送页）</span>
<span style="color: #000000;">methods:{
    uurl(){
      </span><span style="color: #0000ff;">this</span>.$router.push({ name:'xiangmu',params:{msg:'params&gt;msg属性值'},query:{gg:'query&gt;gg 属性值'<span style="color: #000000;">} });
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">接收页的路由表</span><span style="color: #008000;">
//</span><span style="color: #008000;">根据实际情况选择写或不写</span>

<span style="color: #008000;">//</span><span style="color: #008000;">mounted函数（接收页）</span>
<span style="color: #000000;">mounted(){
</span><span style="color: #008000;">//</span><span style="color: #008000;">路由表没有添加params的属性情况</span><span style="color: #008000;">
//</span><span style="color: #008000;">1、则地址栏接收不到params，但是页面实际是可以收到的</span><span style="color: #008000;">
//</span><span style="color: #008000;">2、地址栏可以正常接收query</span>
      alert(<span style="color: #0000ff;">this</span><span style="color: #000000;">.$route.params.msg);
      alert(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.$route.query.gg);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>建议：不带参数时用path跳转，带参数时用name跳转</p>
