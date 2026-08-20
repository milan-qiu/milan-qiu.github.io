---
title: "04、ES6 Promise"
date: "2020-04-30 09:27:00"
updated: "2020-04-30 09:32:00"
tags:
categories:
description: >-
  回调与promise 回调 //回调： 用于请求数据。每次调用都传入一个回调函数 function hui(bb){ bb && bb(); //判断传进来的bb 是否存在，若存在是否函数，若函数就调用 } hui(function(){ console.log(1); hui(function()
---

<h2>回调与promise</h2>
<h3>&nbsp;回调</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">回调： 用于请求数据。每次调用都传入一个回调函数</span>

<span style="color: #0000ff;">function</span><span style="color: #000000;"> hui(bb){
    bb </span>&amp;&amp; bb();  <span style="color: #008000;">//</span><span style="color: #008000;">判断传进来的bb 是否存在，若存在是否函数，若函数就调用</span>
<span style="color: #000000;">}
hui(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    console.log(</span>1<span style="color: #000000;">);

    hui(</span><span style="color: #0000ff;">function</span>(){ <span style="color: #008000;">//</span><span style="color: #008000;">这里面可以调用console.log(1)那一层的内容</span>
        console.log(2<span style="color: #000000;">);

        hui(</span><span style="color: #0000ff;">function</span>(){<span style="color: #008000;">//</span><span style="color: #008000;">这里面可以调用console.log(2)那一层的内容</span>
            console.log(3<span style="color: #000000;">);
        });
    });
});
</span><span style="color: #008000;">//</span><span style="color: #008000;">这样嵌套地调用维护成本高，个人建议两层以上就不要用这种方法了，改用promise</span></pre>
</div>
<p>&nbsp;</p>
<h3>Promise</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">promise： 用于请求数据</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> hui(){
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise(bb =&gt;<span style="color: #000000;"> { bb(); });
}

hui()
.then(</span><span style="color: #0000ff;">function</span>(){    <span style="color: #008000;">//</span><span style="color: #008000;">每一个Promise都有一个then方法</span>
    console.log(1<span style="color: #000000;">);
    </span><span style="color: #0000ff;">return</span> hui();    <span style="color: #008000;">//</span><span style="color: #008000;">若下面还有用到then，必须返回Promise实例，而Promise实例就在hui()中</span>
<span style="color: #000000;">})
.then(</span><span style="color: #0000ff;">function</span>(){  <span style="color: #008000;">//</span><span style="color: #008000;">then里面的function对应的是，hui()里面的bb</span>
    console.log(2<span style="color: #000000;">);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> hui();
})
.then(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(){
    console.log(</span>3);     <span style="color: #008000;">//</span><span style="color: #008000;">下面没有then了，就不必返回Promise实例</span>
})</pre>
</div>
<p>&nbsp;</p>
<h3>信任问题&nbsp;</h3>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">一般回调</span><span style="color: #008000;">
//</span><span style="color: #008000;">如调用第三方库，并传入一个回调</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> methods(cb){
    </span><span style="color: #008000;">//</span><span style="color: #008000;">未按照所想预期执行回调</span>
    setTimeout(<span style="color: #0000ff;">function</span><span style="color: #000000;">(){
        </span><span style="color: #008000;">//</span><span style="color: #008000;">现在执行一下回调</span>
        cb&amp;&amp;<span style="color: #000000;">cb();
        </span><span style="color: #008000;">//</span><span style="color: #008000;">不明情况下又执行了一下回调，最后导致程序出错</span>
        cb&amp;&amp;<span style="color: #000000;">cb();
    },</span>2000<span style="color: #000000;">)
}</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">Promise</span><span style="color: #008000;">
//</span><span style="color: #008000;">Promise一旦确认为成功或失败 就不能被更改</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> methods(){
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise(resolve =&gt;<span style="color: #000000;"> { 
        setTimeout(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(){
            resolve();    </span><span style="color: #008000;">//</span><span style="color: #008000;">成功一次只能调用一次Promise里面的回调</span>
            resolve();    <span style="color: #008000;">//</span><span style="color: #008000;">第二次调用是不会成功的</span>
        },2000<span style="color: #000000;">)
    })
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;错误处理</h3>
<p>&nbsp;//promise有成功也有失败。</p>
<h4>&nbsp;失败的回调（不传参）</h4>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">不传参</span><span style="color: #008000;">
//</span><span style="color: #008000;">promise失败的情况下的处理</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> methods(val){
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise((resolve,reject) =&gt;<span style="color: #000000;"> {
        </span><span style="color: #0000ff;">if</span>(val){ <span style="color: #008000;">//</span><span style="color: #008000;">若val为true，则执行成功做的事</span>
<span style="color: #000000;">            resolve();
        }</span><span style="color: #0000ff;">else</span>{ <span style="color: #008000;">//</span><span style="color: #008000;">若val为false，则执行失败做的事</span>
<span style="color: #000000;">            reject();
        }
    });
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">then(resolve,reject)</span><span style="color: #008000;">
//</span><span style="color: #008000;">then方法中，第二个回调是失败时做的事</span>
methods(<span style="color: #0000ff;">false</span><span style="color: #000000;">)
.then(()</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'成功'<span style="color: #000000;">);
},()</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'失败'<span style="color: #000000;">);
})</span></pre>
</div>
<p>&nbsp;</p>
<h4>&nbsp;失败的回调（传参）</h4>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">传参</span><span style="color: #008000;">
//</span><span style="color: #008000;">promise失败的情况下的处理</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> methods(val){
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise((resolve,reject) =&gt;<span style="color: #000000;"> {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;">(val){
            resolve({name:</span>'萱萱',age:18}); <span style="color: #008000;">//</span><span style="color: #008000;">成功时传入的参数，只能传一个参数。若传的是对象，里面可包含多个数据</span>
        }<span style="color: #0000ff;">else</span><span style="color: #000000;">{
            reject(</span>'404');  <span style="color: #008000;">//</span><span style="color: #008000;">失败时传入的参数。同样只能传一个参数</span>
<span style="color: #000000;">        }
    });
}

methods(</span><span style="color: #0000ff;">false</span><span style="color: #000000;">)
.then(success</span>=&gt;<span style="color: #000000;">{
    console.log(success); </span><span style="color: #008000;">//</span><span style="color: #008000;">成功时接收的参数</span>
},fail=&gt;<span style="color: #000000;">{
    console.log(fail);</span><span style="color: #008000;">//</span><span style="color: #008000;">失败时接收的参数</span>
})</pre>
</div>
<p>&nbsp;</p>
<h4>&nbsp;catch</h4>
<p>//捕获错误，并对其进行处理</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">catch</span><span style="color: #008000;">
//</span><span style="color: #008000;">使用catch的实例方法，可以捕获错误</span>
<span style="color: #000000;">
methods(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
.then(()</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'先成功后失败'<span style="color: #000000;">);
    </span><span style="color: #0000ff;">return</span> methods(<span style="color: #0000ff;">false</span>); <span style="color: #008000;">//</span><span style="color: #008000;">若返回了false，后面没有与之对应的回调或catch就会出错</span>
<span style="color: #000000;">})

.then(()</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'第一个回调是成功执行的，所以这条语句会被跳过'<span style="color: #000000;">);
})

</span><span style="color: #008000;">//</span><span style="color: #008000;"> //方法一</span><span style="color: #008000;">
//</span><span style="color: #008000;"> .then(()=&gt;{  //成功的回调</span><span style="color: #008000;">
//</span><span style="color: #008000;">     console.log('这里的成功回调也不会被执行');    </span><span style="color: #008000;">
//</span><span style="color: #008000;"> },()=&gt;{  //失败的回调</span><span style="color: #008000;">
//</span><span style="color: #008000;">     console.log('若前面的错误回调一直没有被执行，那么就会延续到这里执行')</span><span style="color: #008000;">
//</span><span style="color: #008000;"> })</span>

<span style="color: #008000;">//</span><span style="color: #008000;">方法二</span>
.<span style="color: #0000ff;">catch</span>(()=&gt;<span style="color: #000000;">{
    console.log(</span>'这条是用来捕获错误用的'<span style="color: #000000;">);
})</span></pre>
</div>
<p>&nbsp;</p>
<h4>finally</h4>
<p>//最后执行的内容</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">finally</span><span style="color: #008000;">
//</span><span style="color: #008000;">无论成功或失败都会执行finally</span>
.<span style="color: #0000ff;">finally</span>(()=&gt;<span style="color: #000000;">{
    console.log(</span>'最后才会执行的内容'<span style="color: #000000;">);
})</span></pre>
</div>
<p>&nbsp;</p>
<h3>promise的三种状态</h3>
<p>//状态的改变不可逆，一旦决议就不能再修改</p>
<p>pending： 进行中</p>
<p>fulfilled：成功</p>
<p>rejected：失败</p>
<p>//一旦从pending变成了fulfilled，或从pending变成了rejected，就不能够更改了&nbsp;</p>
<p>&nbsp;</p>
<h3>&nbsp;Promise.all</h3>
<p>//将多个promise实例，包装成一个新的promise实例。</p>
<p>即 Promise.all ([ promise1 , promise2 ] )</p>
<p>1、当promise里面<strong>全部决议为成功</strong>，<strong>promise.all才会决议为成功</strong>，并将<strong>resolve所带的参数</strong>，按顺序<strong>组成一个数组返回</strong></p>
<p>2、当promise里面<strong>有一个决议为失败</strong>，<strong>promise.all就会决议为失败</strong>，并将决议<strong>失败的rejected所带的参数</strong>，按顺序<strong>组成一个数组返回</strong></p>
<p>3、当 Promise.all 为空数组的时候，就会决议为成功，即 Promisse.all ([ ])</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> Promise.all</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> getData1(val){
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise((resolve,reject)=&gt;<span style="color: #000000;">{
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (val) {
            resolve(</span>'data1'<span style="color: #000000;">);
        }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
            reject(</span>'data1 error'<span style="color: #000000;">)
        }
    })
}
</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> getData2(val){
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise((resolve,reject)=&gt;<span style="color: #000000;">{
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (val) {
            resolve(</span>'data2'<span style="color: #000000;">);
        }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
            reject(</span>'data2 error'<span style="color: #000000;">)
        }
    })
}
</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> getData3(val){
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Promise((resolve,reject)=&gt;<span style="color: #000000;">{
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (val) {
            resolve(</span>'data3'<span style="color: #000000;">);
        }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
            reject(</span>'data3 error'<span style="color: #000000;">)
        }
    })
}

let p </span>= Promise.all([getData1(<span style="color: #0000ff;">true</span>),getData2(<span style="color: #0000ff;">true</span>),getData3(<span style="color: #0000ff;">true</span><span style="color: #000000;">)]);

p.then(arr</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'当所有promise实例决议为true时，才输出'<span style="color: #000000;">)
    console.log(arr);
},e</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'当某一项为false时，输出某一项的reject信息'<span style="color: #000000;">);
    console.log(</span>'若有两项错误信息，则输出最先出现的那个错误信息'<span style="color: #000000;">);
    console.log(e);
})</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">当promise.all里为空数组时，决议为true</span>
let p =<span style="color: #000000;"> Promise.all([]);

p.then(arr</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'当promise.all里为空数组时，决议为true'<span style="color: #000000;">)
    console.log(arr);
},e</span>=&gt;<span style="color: #000000;">{
    console.log(e);
})</span></pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;Promise.race</h3>
<p>&nbsp;//在promise的实例中，只要有一个返回成功/失败，那么promise.race就为成功/失败</p>
<p>//若promise.race接收的是空数组，则会永远地挂起</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">Promise.race</span><span style="color: #008000;">
//</span><span style="color: #008000;">在promise的实例中，只要有一个返回成功/失败，那么promise.race就为成功/失败</span>
const promise1 = <span style="color: #0000ff;">new</span> Promise(<span style="color: #0000ff;">function</span><span style="color: #000000;">(resolve, reject) {
    setTimeout(resolve, </span>500, 'one'<span style="color: #000000;">);
});

const promise2 </span>= <span style="color: #0000ff;">new</span> Promise(<span style="color: #0000ff;">function</span><span style="color: #000000;">(resolve, reject) {
    setTimeout(resolve, </span>100, 'two'<span style="color: #000000;">);
});

Promise.race([promise1, promise2]).then(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(value) {
  console.log(value);
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 两个都是成功的，但是promise2反应速度更快，所以这里的就是two</span>
<span style="color: #000000;">});
</span><span style="color: #008000;">//</span><span style="color: #008000;"> expected output: "two"</span></pre>
</div>
<p>&nbsp;</p>
<h3>Promise.resolve() 与 Promise.reject()</h3>
<p>//常用来生成已经被决议为成功或失败的Promise实例</p>
<h4>Promise.resolve()传递参数时，有3种情况</h4>
<p>第一种，传递普通值</p>
<div class="cnblogs_code">
<pre>let p1 = <span style="color: #0000ff;">new</span> Promise(resolve=&gt;{ <span style="color: #008000;">//</span><span style="color: #008000;">两条语句的效果都一模一样</span>
    resolve('成功'<span style="color: #000000;">);
});
let p2 </span>= Promise.resolve('成功'); <span style="color: #008000;">//</span><span style="color: #008000;">两条语句的效果都一模一样</span></pre>
</div>
<p>&nbsp;</p>
<p>第二种，传递promise实例</p>
<div class="cnblogs_code">
<pre>let p = <span style="color: #0000ff;">new</span> Promise(resolve=&gt;<span style="color: #000000;">{
    resolve(</span>'好'<span style="color: #000000;">);
})
let pp </span>= Promise.resolve(p); <span style="color: #008000;">//</span><span style="color: #008000;">直接将p的promise实例返回给pp，即 p === pp</span><span style="color: #000000;">
pp.then(data</span>=&gt;<span style="color: #0000ff;">void</span> console.log(data)); <span style="color: #008000;">//</span><span style="color: #008000;">这里接收的参数是p里面resolve的参数</span></pre>
</div>
<p>&nbsp;</p>
<p>第三种，传递一个thenable对象</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">thenable就是具有then方法的对象</span>
let obj =<span style="color: #000000;"> {
    then(cb){
        console.log(</span>'obj里面的then被执行了'<span style="color: #000000;">);
        cb(</span>'这里相当于resolve传递参数'<span style="color: #000000;">);
    },
    oth(){
        console.log(</span>'其他'<span style="color: #000000;">);
    }
};
</span><span style="color: #008000;">//</span><span style="color: #008000;">立即执行then方法</span>
Promise.resolve(obj).then(data =&gt;<span style="color: #000000;">{
    console.log(data);
});</span></pre>
</div>
<p>//不管什么值，只要Promise.resolve包一下就成为了promise实例了。</p>
<p>&nbsp;</p>
<h4>Promise.reject()</h4>
<p>//只要决议为失败，会按照原来的原封不动地传递过来</p>
<div class="cnblogs_code">
<pre>Promise.reject({then() {console.log('并不会解析这条内容，只负责传递'<span style="color: #000000;">);} })
.then(()</span>=&gt;<span style="color: #000000;">{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">这里是决议成功的函数，这里用不到</span>
},e=&gt;<span style="color: #000000;">{
    console.log(e); </span><span style="color: #008000;">//</span><span style="color: #008000;">这里输出的是then函数本身，不会进行解析</span>
});</pre>
</div>
<p>&nbsp;</p>
<h3>&nbsp;Promise同步与异步</h3>
<p>&nbsp;//promise决议之后，异步地执行后面地事情，异步任务在同步任务之后执行。如then里面就是异步任务。</p>
<p>根据这个特性，可将同步任务转为异步任务</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span><span style="color: #000000;"> createAsyncTask(syncTack){
    </span><span style="color: #0000ff;">return</span> Promise.resolve(syncTack).then(syncTack=&gt;<span style="color: #000000;">{
        syncTack()
    });
}

createAsyncTask(()</span>=&gt;<span style="color: #000000;">{
    console.log(</span>'我变成了异步任务'<span style="color: #000000;">);
    </span><span style="color: #0000ff;">return</span> 1+1<span style="color: #000000;">;
}).then(res</span>=&gt;<span style="color: #000000;">{
    console.log(res);
});

console.log(</span>'我是同步任务');</pre>
</div>
<p>&nbsp;</p>
