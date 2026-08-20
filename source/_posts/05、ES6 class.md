---
title: "05、ES6 class"
date: "2020-05-06 15:36:00"
updated: "2020-05-06 15:38:00"
tags:
categories:
description: >-
  类与对象 OOP-面向对象开发（核心是封装） es5函数封装 //面向过程的封装： 封装一个自执行的匿名函数，这样内部的各种属性和方法就不会暴露在全局下面。面向过程可以暂时理解为函数 es6的类封装 //类相当于一个工厂，只要给适当的参数就会生产出对应的对象。//构造函数相当于接头人，负责接收参数，
---

<h2>类与对象</h2>
<p>OOP-面向对象开发（核心是封装）</p>
<h3>es5函数封装</h3>
<p>//面向过程的封装： 封装一个自执行的匿名函数，这样内部的各种属性和方法就不会暴露在全局下面。面向过程可以暂时理解为函数</p>
<h3>es6的类封装</h3>
<p>//类相当于一个工厂，只要给适当的参数就会生产出对应的对象。<br />//构造函数相当于接头人，负责接收参数，有固定名字： constructor<br />//实例化相当于生产的过程，就是类创建对象的过程</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">class car {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">constructor构造函数用来接收参数</span>
    constructor([name,color]){ <span style="color: #008000;">//</span><span style="color: #008000;">这里函数的写法，跟对象里的简洁表示法一样</span>
        <span style="color: #0000ff;">this</span>.name = name; <span style="color: #008000;">//</span><span style="color: #008000;">this是在一个类中能被访问的一个关键字</span>
        <span style="color: #0000ff;">this</span>.color = color; <span style="color: #008000;">//</span><span style="color: #008000;">若没有this，下面实例化完的对象就访问不到这里的属性</span>
        <span style="color: #0000ff;">this</span>.number = 0<span style="color: #000000;">;
        console.log(</span>'开始接收参数'<span style="color: #000000;">);
        console.log(name,color);
    }

    add(){
        </span><span style="color: #0000ff;">this</span>.number += 1;    <span style="color: #008000;">//</span><span style="color: #008000;">这里可以对constructor里面的参数进行更改</span>
        console.log(<span style="color: #0000ff;">this</span><span style="color: #000000;">.number);
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">只要class准备好了就可以实例化了</span>
const che =  <span style="color: #0000ff;">new</span> car(['奔驰','红色']); <span style="color: #008000;">//</span><span style="color: #008000;">这里相当于调用constructor，括号里面可以传递参数</span>
<span style="color: #000000;">
console.log(che); </span><span style="color: #008000;">//</span><span style="color: #008000;">上面有了this的关键字，这里就能访问到属性了</span>

<span style="color: #008000;">//</span><span style="color: #008000;">实例化之后就可以调用里面的方法了</span>
che.add();</pre>
</div>
<p>&nbsp;</p>
<h3>class的三大特性</h3>
<p>一、封装</p>
<p>二、继承</p>
<p>三、多态： 同一个接口不同的表现</p>
<p>&nbsp;</p>
<h2>静态属性与静态方法</h2>
<p>1、不会被类实例所拥有的属性与方法，只是自身拥有。</p>
<p>2、只能通过类调用。</p>
<h3>&nbsp;</h3>
<h3>静态属性的定义与调用</h3>
<h4>定义</h4>
<p>第一种，在类里面，在constructor前面</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">定义静态属性一： 在类里面</span><span style="color: #008000;">
//</span><span style="color: #008000;">static 属性名 = 属性值</span>
static stt = 'constructor前面定义的静态属性';<br /><br />//修改静态属性</pre>
<p>　constructor(){<br />	　　　//对第一种方式的，静态属性进行修改。<br />	　　　//必须先实例化再调用才生效<br />	　　　haha.stt = '01234';<br />　}</p>













</div>
<p>&nbsp;</p>
<p>第二种，在类外面</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 定义静态属性二： 在类外面</span><span style="color: #008000;">
//</span><span style="color: #008000;"> 定义静态属性： 类名 . 属性名 = 属性值 </span>
haha.str = '静态属性'; </pre>
</div>
<p>&nbsp;</p>
<h4>调用</h4>
<div class="cnblogs_code">
<pre>console.log(haha.stt); <span style="color: #008000;">//</span><span style="color: #008000;">调用静态属性，类名 . 静态属性名。</span>
console.log(haha.str); <span style="color: #008000;">//</span><span style="color: #008000;">调用静态属性，类名 . 静态属性名。</span></pre>
</div>
<p>&nbsp;</p>
<h3>静态方法的定义与调用</h3>
<h4>定义</h4>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">定义普通方法</span>
<span style="color: #000000;">bb(){
    console.log(</span>'静态方法跟普通方法重名是没关系的，互不影响'<span style="color: #000000;">);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">定义静态方法</span>
<span style="color: #000000;">static bb(name){
    console.log(</span>'我是静态方法，只有class才能调用。传进来的参数是：' +<span style="color: #000000;"> name);
}</span></pre>
</div>
<p>&nbsp;</p>
<h4>调用</h4>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">调用静态方法，只有该class才能调用静态方法</span>
haha.bb('大比');  <span style="color: #008000;">//</span><span style="color: #008000;">类名 . 静态方法名</span></pre>
</div>
<p>&nbsp;</p>
<h2>类表达式</h2>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">类表达式</span>
const p = class a{  <span style="color: #008000;">//</span><span style="color: #008000;">若不需要，a可以省略</span>
<span style="color: #000000;">    constructor(){
        console.log(</span>'这里p是 === a的，a仅限于内部使用'<span style="color: #000000;">);
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> new p();</span>


<span style="color: #008000;">//</span><span style="color: #008000;">类的声明</span>
<span style="color: #000000;">class bb{
    constructor(){
        console.log(</span>'类的声明'<span style="color: #000000;">);
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> new bb();</span>


<span style="color: #008000;">//</span><span style="color: #008000;">类的自执行</span>
const aa = <span style="color: #0000ff;">new</span><span style="color: #000000;"> class p{
    constructor(){
        p.a </span>= 26<span style="color: #000000;">;
        console.log(p.a);
    }
    
}()</span></pre>
</div>
<p>&nbsp;</p>
<h2>getter、setter</h2>
<p>//类似给属性提供钩子。在获取属性和设置属性的时候做一些额外的事情</p>
<p>&nbsp;</p>
<h3>ES5的getter、setter</h3>
<p>1、在字面量中书写get、set方法</p>
<div class="cnblogs_code">
<pre>const obj =<span style="color: #000000;"> {
    _name:</span>'123'<span style="color: #000000;">,
    get name(){     </span><span style="color: #008000;">//</span><span style="color: #008000;">获取name属性</span>
        console.log('这是获取name的操作'); <span style="color: #008000;">//</span><span style="color: #008000;">除了返回name之外，还可以做其他额外的操作</span>
        <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">._name;
    },
    set name(val){  </span><span style="color: #008000;">//</span><span style="color: #008000;">设置name属性</span>
        <span style="color: #0000ff;">this</span>._name =<span style="color: #000000;"> val;
    }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置name，实际上是设置_name</span>
obj.name = '设置name，会自动调用set name方法'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取name，实际上是访问_name</span>
<span style="color: #000000;">console.log(obj.name);

</span><span style="color: #008000;">//</span><span style="color: #008000;">name属性名 跟 get、set方法名不可以重名。 若重名会报错，栈内存溢出</span><span style="color: #008000;">
//</span><span style="color: #008000;">先触发get name，里面this.name访问了name，访问了name又会触发get name ......</span></pre>
</div>
<p>&nbsp;</p>
<p>2、Object.defineProperty</p>
<div class="cnblogs_code">
<pre>const obj =<span style="color: #000000;"> {
    _age : </span>2<span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">设置/添加属性</span>
Object.defineProperty(obj,'age',{  <span style="color: #008000;">//</span><span style="color: #008000;">这里同样不能重名</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">value : 88,</span>
    get : <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
        console.log(</span>'正在使用get方法'<span style="color: #000000;">);
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span>._age; <span style="color: #008000;">//</span><span style="color: #008000;">这里同样不能重名</span>
<span style="color: #000000;">    },
    set : </span><span style="color: #0000ff;">function</span><span style="color: #000000;">(val){
        console.log(</span>'正在使用set方法'<span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>._age = val; <span style="color: #008000;">//</span><span style="color: #008000;">这里同样不能重名</span>
<span style="color: #000000;">    }
});
</span><span style="color: #008000;">//</span><span style="color: #008000;">第一个参数： obj是表示要操作的对象</span><span style="color: #008000;">
//</span><span style="color: #008000;">第二个参数： 'age'表示需要设置/添加的属性</span><span style="color: #008000;">
//</span><span style="color: #008000;">第三个参数： 一个对象，里面是对属性的描述</span><span style="color: #008000;">
//</span><span style="color: #008000;">value是属性的值，即第二个参数的值。</span><span style="color: #008000;">
//</span><span style="color: #008000;">是否可以枚举： enumerable:true 。默认是false，不可以被遍历出来</span><span style="color: #008000;">
//</span><span style="color: #008000;">描述还可以添加是否可读。</span>

<span style="color: #008000;">//</span><span style="color: #008000;"> console.log(obj); //里面多出了一个age属性。不过默认age属性是不可以被遍历出来的</span>

<span style="color: #008000;">//</span><span style="color: #008000;">修改age</span>
obj.age = 88<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取age</span>
console.log(obj.age);</pre>
</div>
<p>&nbsp;</p>
<h3>ES6的class中，getter、setter</h3>
<div class="cnblogs_code">
<pre><span style="color: #000000;">class obj{
    constructor(){
        </span><span style="color: #0000ff;">this</span>._address = '北京'<span style="color: #000000;">;
    }
    get address(){
        console.log(</span>'class里面的get操作'<span style="color: #000000;">);
        </span><span style="color: #0000ff;">return</span> `我家住在${<span style="color: #0000ff;">this</span><span style="color: #000000;">._address}`;
    }
    set address(val){
        console.log(</span>'class里面的set操作'<span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>._address =<span style="color: #000000;"> val;
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">首先需要实例化</span>
const p = <span style="color: #0000ff;">new</span><span style="color: #000000;"> obj();

</span><span style="color: #008000;">//</span><span style="color: #008000;">修改address</span>
p.address = '上海'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取address</span>
console.log(p.address);</pre>
</div>
<p>&nbsp;</p>
<h3>name属性 与 new.target属性</h3>
<h4>name属性</h4>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">name属性获取class类名</span>
<span style="color: #000000;">class bb {}
console.log(bb.name); </span><span style="color: #008000;">//</span><span style="color: #008000;">类名是bb</span>
<span style="color: #000000;">
const aa </span>=<span style="color: #000000;"> class {}
console.log(aa.name); </span><span style="color: #008000;">//</span><span style="color: #008000;">类名是aa</span>
<span style="color: #000000;">
const cc </span>=<span style="color: #000000;"> class dd{}
console.log(cc.name); </span><span style="color: #008000;">//</span><span style="color: #008000;">类名是dd</span></pre>
</div>
<p>&nbsp;</p>
<h4>new.target属性</h4>
<p>//表示该类/函数自身。只有在类 或 构造函数/函数 里面才可以访问</p>
<div class="cnblogs_code">
<pre>ass Car{ <span style="color: #008000;">//</span><span style="color: #008000;">类使用</span>
<span style="color: #000000;">    constructor(){
        console.log(</span><span style="color: #0000ff;">new</span>.target); <span style="color: #008000;">//</span><span style="color: #008000;">打印出这个类本身</span>
<span style="color: #000000;">    }
}
</span><span style="color: #0000ff;">new</span> Car(); <span style="color: #008000;">//</span><span style="color: #008000;">new后面的Car()，就是new.target属性</span>


<span style="color: #0000ff;">function</span> ccr(){ <span style="color: #008000;">//</span><span style="color: #008000;">构造函数 或 普通函数都可以使用</span>
    <span style="color: #008000;">//</span><span style="color: #008000;">判断是否使用new关键字调用</span>
    <span style="color: #0000ff;">if</span>(ccr == <span style="color: #0000ff;">new</span>.target){ <span style="color: #008000;">//</span><span style="color: #008000;">还可以这样判断(this instanceof ccr)，详情看下面构造函数流程</span>
        console.log(<span style="color: #0000ff;">new</span>.target); <span style="color: #008000;">//</span><span style="color: #008000;">只有构造函数调用，才能正常使用new.target</span>
    }<span style="color: #0000ff;">else</span><span style="color: #000000;">{
        </span><span style="color: #0000ff;">throw</span> Error('必须用new关键字调用'<span style="color: #000000;">);
    }
}
</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> ccr();
</span><span style="color: #008000;">//</span><span style="color: #008000;">构造函数调用 跟 普通函数调用 走的流程不一样</span><span style="color: #008000;">
//</span><span style="color: #008000;">1、构造函数this会先指向一个新的空对象</span><span style="color: #008000;">
//</span><span style="color: #008000;">2、构造函数的prototype属性会成为 空对象的原型<br />//3、this赋值给这个空对象<br />//4、执行函数</span><span style="color: #008000;">
//5</span><span style="color: #008000;">、若该函数没有返回值的话，则返回this。即之前那个空对象</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>ES5模拟类</h3>
<p>1、构造函数this会先指向一个新的空对象</p>
<p>2、构造函数的prototype属性会成为 空对象的原型</p>
<p>3、this赋值给这个空对象</p>
<p>4、执行函数</p>
<p>5、若该函数没有返回值的话，则返回this。即之前那个空对象</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">将构造函数的流程封装成一个函数</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> Constructor(fn,args){
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 1、构造函数this会先指向一个新的空对象</span>
    <span style="color: #008000;">//</span><span style="color: #008000;"> 2、构造函数的prototype属性会成为 空对象的原型</span>
    <span style="color: #0000ff;">var</span> _this =<span style="color: #000000;"> Object.create(fn.prototype);
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var _this = Object.create(fn.prototype);</span>

    <span style="color: #008000;">//</span><span style="color: #008000;"> 3、this赋值给这个空对象</span>
    <span style="color: #0000ff;">var</span> res =<span style="color: #000000;"> fn.apply(_this,args);
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var res = fn.apply(_this, args);</span>

    <span style="color: #008000;">//</span><span style="color: #008000;"> 4、执行函数 </span>
    <span style="color: #008000;">//</span><span style="color: #008000;"> 5、若该函数没有返回值的话，则返回this。即之前那个空对象</span>
    <span style="color: #0000ff;">return</span> res ?<span style="color: #000000;"> res : _this;
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> return res ? res : _this;</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;">构建一个普通函数</span>
<span style="color: #0000ff;">function</span><span style="color: #000000;"> Person(name,age){
    </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
    </span><span style="color: #0000ff;">this</span>.age =<span style="color: #000000;"> age;
}
Person.prototype.say </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
    console.log(`我叫${</span><span style="color: #0000ff;">this</span>.name}，我今年${<span style="color: #0000ff;">this</span><span style="color: #000000;">.age}岁了`);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">将 普通函数 转为 构造函数</span>
<span style="color: #0000ff;">var</span> ren = Constructor(Person,['张三',88<span style="color: #000000;">]);
console.log(ren);</span></pre>
</div>
<p>&nbsp;</p>
<h3>类的继承</h3>
<div class="cnblogs_code">
<pre>class fu{    <span style="color: #008000;">//</span><span style="color: #008000;">定义父类</span>
<span style="color: #000000;">    constructor(name,sex,age){
        </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
        </span><span style="color: #0000ff;">this</span>.sex =<span style="color: #000000;"> sex;
        </span><span style="color: #0000ff;">this</span>.age =<span style="color: #000000;"> age;
    }
    shuo(){     </span><span style="color: #008000;">//</span><span style="color: #008000;">定义父类的方法</span>
        console.log(`我的名字是${<span style="color: #0000ff;">this</span>.name}，性别是${<span style="color: #0000ff;">this</span>.sex}，年龄是${<span style="color: #0000ff;">this</span><span style="color: #000000;">.age}`);
    }
}

class zi extends fu{    </span><span style="color: #008000;">//</span><span style="color: #008000;">定义子类，并继承父类</span>
    constructor(name,sex,age,skill){    <span style="color: #008000;">//</span><span style="color: #008000;">接收父类的参数 和 子类的参数</span>
        super(name,sex,age);    <span style="color: #008000;">//</span><span style="color: #008000;">给父类传入参数</span>
        <span style="color: #0000ff;">this</span>.skill =<span style="color: #000000;"> skill;
    }
    jineng(){  </span><span style="color: #008000;">//</span><span style="color: #008000;">定义子类的方法</span>
        console.log(`我的技能有${<span style="color: #0000ff;">this</span><span style="color: #000000;">.skill}`);
    }
}

const person </span>= <span style="color: #0000ff;">new</span> zi('小蝴蝶','女',3,'嚎啕大哭'); <span style="color: #008000;">//</span><span style="color: #008000;">实例化子类，并传入参数</span>
<span style="color: #000000;">
person.shuo();    </span><span style="color: #008000;">//</span><span style="color: #008000;">调用父类的方法</span>
<span style="color: #000000;">
person.jineng();    </span><span style="color: #008000;">//</span><span style="color: #008000;">调用子类方法</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>super关键字的其他内容</h3>
<h4>作为父类构造函数调用</h4>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">在继承中有使用到，在调用之后子类就会有父类的属性和方法。</span><span style="color: #008000;">
//</span><span style="color: #008000;">（相当于把子类的this放到父类的构造函数中运行一遍，后继续走子类的构造函数）</span>
<span style="color: #000000;">class fu{
    constructor(name){
        </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
    }
}
class zi extends fu{
    constructor(name,sex){
        super(name);
        </span><span style="color: #0000ff;">this</span>.sex =<span style="color: #000000;"> sex;
    }
    methods(){
        console.log(`我的名字是${</span><span style="color: #0000ff;">this</span>.name}，我是${<span style="color: #0000ff;">this</span><span style="color: #000000;">.sex}生。`);
    }
}
const child </span>= <span style="color: #0000ff;">new</span> zi('大白','女'<span style="color: #000000;">);
child.methods();</span></pre>
</div>
<h4>&nbsp;</h4>
<h4>作为对象的方式调用。</h4>
<p>//在调用super，父类的this始终是子类的this</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">在非静态方法中访问super，访问的是父类原型</span>
<span style="color: #000000;">class fu{
    fusay(){
        console.log(</span>'您好！'<span style="color: #000000;">);
    }
}

class zi extends fu{
    zisay(){
        console.log(super.fusay); </span><span style="color: #008000;">//</span><span style="color: #008000;">这样的话调用子类的zisay就会输出父类的fusay函数本身。</span>
        <span style="color: #008000;">//</span><span style="color: #008000;">若要执行父类的fusay，这里也可以直接调用，如： super.fusay()</span>
<span style="color: #000000;">    }
}
const child </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> zi();
child.zisay(); </span><span style="color: #008000;">//</span><span style="color: #008000;">作为对象调用的时候，不使用super也可以调用父类的方法</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">在静态方法中访问super，访问的是父类</span>
<span style="color: #000000;">class fu{
}
fu.total </span>= 898<span style="color: #000000;">;

class zi extends fu{
    static tot(){
        console.log(super.total);
    }
}
zi.tot();</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">验证： 调用super时，父类的this始终是子类的this</span>
<span style="color: #000000;">class fu{
    check(_this){
        console.log(_this </span>=== <span style="color: #0000ff;">this</span>); <span style="color: #008000;">//</span><span style="color: #008000;">接收子类的this，并把子类的this与父类的this相比较</span>
<span style="color: #000000;">    }
}
class zi extends fu{
    use(){
        super.check(</span><span style="color: #0000ff;">this</span>); <span style="color: #008000;">//</span><span style="color: #008000;">调用父类check方法，并把子类的this传过去</span>
<span style="color: #000000;">    }
}
const yan </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> zi();
yan.use();    </span><span style="color: #008000;">//</span><span style="color: #008000;">true</span></pre>
</div>
<p>&nbsp;</p>
<h3>简单的多态</h3>
<p>//同一个接口在不同的情况下，做不同的事情。即相同的接口，不同的表现</p>
<p>//好处： 提高类的扩充性和灵活性。还可以暴露接口，让子类完成父类不需要完成的内容。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">class human{
    say(){
        console.log(</span>'我是人'<span style="color: #000000;">);
    }
}
class man extends human{  </span><span style="color: #008000;">//</span><span style="color: #008000;">多态必须要通过继承来实现。子类写一个父类同名的方法即可达到覆盖的效果</span>
<span style="color: #000000;">    say(){
        console.log(</span>'我是男人'<span style="color: #000000;">);
    }
}
class woman extends human{
    say(){
        console.log(</span>'我是女人'<span style="color: #000000;">);
        super.say();  </span><span style="color: #008000;">//</span><span style="color: #008000;">同样还可以调用父类的say方法</span>
<span style="color: #000000;">    }
}

</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> man().say();
</span><span style="color: #0000ff;">new</span> woman().say();</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>重载</h3>
<p>//根据函数的参数类型、参数个数，让函数做不一样的事情</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">class simpleCalc{
    addCale(...args){
        </span><span style="color: #0000ff;">if</span>(args.length &lt; 2<span style="color: #000000;">){
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.donot();
        }</span><span style="color: #0000ff;">else</span><span style="color: #000000;">{
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.add(args);
        }
    }
    donot(){
        console.log(</span>'参数不够，不执行'<span style="color: #000000;">);
    }
    add(args){
        console.log(args.reduce(</span><span style="color: #0000ff;">function</span>(a,b){<span style="color: #0000ff;">return</span> a+<span style="color: #000000;">b}));
    }
}
</span><span style="color: #0000ff;">new</span> simpleCalc().addCale(1);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>ES5中的继承</h3>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span> P(){  <span style="color: #008000;">//</span><span style="color: #008000;">父函数</span>
    <span style="color: #0000ff;">this</span>.name = '萌萌'<span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.sex = '女'<span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.say = <span style="color: #0000ff;">function</span><span style="color: #000000;">(){
        console.log(</span>'哈哈哈'<span style="color: #000000;">);
    }
}
P.prototype.test </span>= <span style="color: #0000ff;">function</span>(){  <span style="color: #008000;">//</span><span style="color: #008000;">原型的属性和方法不可通过call继承</span>
    console.log('我是P的原型方法'<span style="color: #000000;">);
}

</span><span style="color: #0000ff;">function</span> C(){  <span style="color: #008000;">//</span><span style="color: #008000;">子函数</span>
    P.call(<span style="color: #0000ff;">this</span>);  <span style="color: #008000;">//</span><span style="color: #008000;">这样就执行了P，并把当前this传过去。这样就继承了父函数的属性和方法，但不包括原型的属性和方法。</span>
    <span style="color: #0000ff;">this</span>.age = 18<span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.address = '北京'<span style="color: #000000;">;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">若需要继承父函数的原型属性和方法，需要</span>
C.prototype = <span style="color: #0000ff;">new</span> P(); <span style="color: #008000;">//</span><span style="color: #008000;">C的prototype 可以访问到 P的prototype</span><span style="color: #008000;">
//</span><span style="color: #008000;">P的实例也就是P函数的prototype属性，所以P的实例可以访问到P.prototype的方法</span>

<span style="color: #0000ff;">var</span> bb = <span style="color: #0000ff;">new</span> C();  <span style="color: #008000;">//</span><span style="color: #008000;">实例化子函数</span>
bb.say();  <span style="color: #008000;">//</span><span style="color: #008000;">成功执行父函数的方法</span>
console.log(bb.address); <span style="color: #008000;">//</span><span style="color: #008000;">成功执行子函数的属性</span>
bb.test();  <span style="color: #008000;">//</span><span style="color: #008000;">成功执行父函数的原型方法</span></pre>
</div>
<p>&nbsp;</p>
