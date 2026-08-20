---
title: "webpack5基本使用"
date: "2021-04-11 17:49:00"
updated: "2021-04-11 17:50:00"
tags:
categories:
description: >-
  参考结构 初始化npm npm init -y 安装webpack： cnpm install --save-dev webpack webpack-cli 打包js const path = require('path'); module.exports = { entry: './src/ind
---

<p>参考结构</p>
<p><img src="https://img2020.cnblogs.com/blog/1680452/202104/1680452-20210411165016246-1537597124.png" alt="" width="251" height="235" loading="lazy" /></p>
<p>&nbsp;</p>
<p>初始化npm</p>
<div class="cnblogs_code">
<pre>npm init -y&nbsp;</pre>
</div>
<p>&nbsp;</p>
<p>安装webpack：</p>
<div class="cnblogs_code">
<pre>cnpm install --save-dev webpack webpack-cli</pre>
</div>
<p>&nbsp;</p>
<p><strong>打包js</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">const</span> path = require(<span style="color: #800000;">'</span><span style="color: #800000;">path</span><span style="color: #800000;">'</span><span style="color: #000000;">);

module.exports  </span>=<span style="color: #000000;"> {
    entry: </span><span style="color: #800000;">'</span><span style="color: #800000;">./src/index.js</span><span style="color: #800000;">'</span>,<span style="color: #008000;">//</span><span style="color: #008000;">多个文件用数组</span>
<span style="color: #000000;">    output: {
        filename: </span><span style="color: #800000;">'</span><span style="color: #800000;">index.js</span><span style="color: #800000;">'</span>,<span style="color: #008000;">//</span><span style="color: #008000;">多个文件用文件夹形式</span>
        path: path.resolve(__dirname, <span style="color: #800000;">'</span><span style="color: #800000;">dist</span><span style="color: #800000;">'</span><span style="color: #000000;">),
        clean: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
    },</span></pre>
<div>&nbsp; &nbsp; &nbsp;devtool:&nbsp;'inline-source-map' //便于定位错误出处</div>
<pre><span style="color: #000000;">}<br />ps: webpack.config.js</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>build<span style="color: #800000;">"</span><span style="color: #800000;">: </span><span style="color: #800000;">"</span>webpack --config webpack.config.js<span style="color: #800000;">"</span><span style="color: #800000;">,</span>
<span style="color: #000000;">
ps: package.json的script命令</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>配置默认打包模板</strong></p>
<div class="cnblogs_code">
<pre>cnpm install --save-dev html-webpack-plugin</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">const</span> HtmlWebpackPlugin = require(<span style="color: #800000;">'</span><span style="color: #800000;">html-webpack-plugin</span><span style="color: #800000;">'</span><span style="color: #000000;">);

plugins: [
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> HtmlWebpackPlugin({ 
        template: </span><span style="color: #800000;">'</span><span style="color: #800000;">./index.html</span><span style="color: #800000;">'</span>,<span style="color: #008000;">//</span><span style="color: #008000;">模板路径</span>
        minify: <span style="color: #0000ff;">true</span> <span style="color: #008000;">//</span><span style="color: #008000;">是否压缩</span>
<span style="color: #000000;">    })
]</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>配置热加载</strong></p>
<div class="cnblogs_code">
<pre>cnpm install --save-dev webpack-dev-server</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">devServer: {
    contentBase: path.join(__dirname, </span><span style="color: #800000;">'</span><span style="color: #800000;">dist</span><span style="color: #800000;">'</span>), <span style="color: #008000;">//</span><span style="color: #008000;">监听编译后的文件夹</span>
    compress: <span style="color: #0000ff;">false</span>, <span style="color: #008000;">//</span><span style="color: #008000;">不压缩</span>
    progress:<span style="color: #0000ff;">true</span>, <span style="color: #008000;">//</span><span style="color: #008000;">显示进度</span>
    port: <span style="color: #800080;">3000</span>,<span style="color: #008000;">//</span><span style="color: #008000;">设置端口</span>
<span style="color: #000000;">},

ps: webpack.config.js</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #800000;">"</span><span style="color: #800000;">serve</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">webpack serve --config webpack.config.js</span><span style="color: #800000;">"</span><span style="color: #000000;">

ps: package.json的script命令</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>配置编译sass</strong></p>
<div class="cnblogs_code">
<pre>cnpm install --save-dev sass sass-loader css-loader style-loader</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">module: {
    rules: [
        {
        test: </span>/\.sass$/<span style="color: #000000;">,
        use: [
            </span><span style="color: #800000;">"</span><span style="color: #800000;">style-loader</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;"> 将 JS 字符串生成为 style 节点</span>
            <span style="color: #800000;">"</span><span style="color: #800000;">css-loader</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;"> 将 CSS 转化成 CommonJS 模块</span>
            <span style="color: #800000;">"</span><span style="color: #800000;">sass-loader</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;"> 将 Sass 编译成 CSS</span>
<span style="color: #000000;">        ],
        },
    ],
}

ps: webpack.config.js</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>import <span style="color: #800000;">"</span><span style="color: #800000;">../scss/index.scss</span><span style="color: #800000;">"</span><span style="color: #000000;">;

ps: 在入口文件进行引入</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>最终，不同场景做不同配置</strong></p>
<div class="cnblogs_code">
<pre>cnpm install --save-dev cross-env</pre>
</div>
<p>&nbsp;</p>
<p>webpack.config.js</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">const</span> path = require(<span style="color: #800000;">'</span><span style="color: #800000;">path</span><span style="color: #800000;">'</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">const</span> HtmlWebpackPlugin = require(<span style="color: #800000;">'</span><span style="color: #800000;">html-webpack-plugin</span><span style="color: #800000;">'</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">const</span> <span style="color: #0000ff;">base</span> =<span style="color: #000000;"> {
    entry: </span><span style="color: #800000;">'</span><span style="color: #800000;">./src/index.js</span><span style="color: #800000;">'</span><span style="color: #000000;">,
    output: {
        filename: </span><span style="color: #800000;">'</span><span style="color: #800000;">index.js</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        path: path.resolve(__dirname, </span><span style="color: #800000;">'</span><span style="color: #800000;">dist</span><span style="color: #800000;">'</span><span style="color: #000000;">),
        clean: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
    },
    module: {
        rules: [
          {
            test: </span>/\.s[ac]ss$/<span style="color: #000000;">i,
            use: [
              </span><span style="color: #800000;">"</span><span style="color: #800000;">style-loader</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;"> 将 JS 字符串生成为 style 节点</span>
              <span style="color: #800000;">"</span><span style="color: #800000;">css-loader</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;"> 将 CSS 转化成 CommonJS 模块</span>
              <span style="color: #800000;">"</span><span style="color: #800000;">sass-loader</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;"> 将 Sass 编译成 CSS</span>
<span style="color: #000000;">            ],
          },
        ],
    }
}

</span><span style="color: #0000ff;">const</span> development =<span style="color: #000000;"> {
    mode: </span><span style="color: #800000;">"</span><span style="color: #800000;">development</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ...</span><span style="color: #0000ff;">base</span><span style="color: #000000;">,
    devtool: </span><span style="color: #800000;">'</span><span style="color: #800000;">inline-source-map</span><span style="color: #800000;">'</span><span style="color: #000000;">,
    devServer: {
        contentBase: path.join(__dirname, </span><span style="color: #800000;">'</span><span style="color: #800000;">dist</span><span style="color: #800000;">'</span><span style="color: #000000;">),
        compress: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">,
        progress:</span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
        port: </span><span style="color: #800080;">3000</span><span style="color: #000000;">,
    },
};

</span><span style="color: #0000ff;">const</span> production =<span style="color: #000000;"> {
    mode: </span><span style="color: #800000;">"</span><span style="color: #800000;">production</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ...</span><span style="color: #0000ff;">base</span><span style="color: #000000;">,
    plugins: [
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> HtmlWebpackPlugin({ 
            template: </span><span style="color: #800000;">'</span><span style="color: #800000;">./index.html</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            minify: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
        })
    ]
}

module.exports </span>= process.env.NODE_ENV === <span style="color: #800000;">'</span><span style="color: #800000;">development</span><span style="color: #800000;">'</span> ? development : production;</pre>
</div>
<p>&nbsp;</p>
<p>package.json</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">webpack</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">version</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1.0.0</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span>: <span style="color: #800000;">""</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">private</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">scripts</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">build</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">cross-env NODE_ENV=production webpack --config webpack.config.js</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">serve</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">cross-env NODE_ENV=development webpack serve --config webpack.config.js</span><span style="color: #800000;">"</span><span style="color: #000000;">
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">keywords</span><span style="color: #800000;">"</span><span style="color: #000000;">: [],
  </span><span style="color: #800000;">"</span><span style="color: #800000;">author</span><span style="color: #800000;">"</span>: <span style="color: #800000;">""</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">license</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ISC</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">devDependencies</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">cross-env</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^7.0.3</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">css-loader</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^5.2.1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">html-webpack-plugin</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^5.3.1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sass</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^1.32.8</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sass-loader</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^11.0.1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">style-loader</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^2.0.0</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">webpack</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^5.31.2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">webpack-cli</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^4.6.0</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">webpack-dev-server</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">^3.11.2</span><span style="color: #800000;">"</span><span style="color: #000000;">
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">dependencies</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}
}</span></pre>
</div>
<p>&nbsp;</p>
