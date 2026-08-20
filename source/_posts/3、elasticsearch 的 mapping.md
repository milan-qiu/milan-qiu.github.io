---
title: "3、elasticsearch 的 mapping"
date: "2022-02-20 11:36:00"
updated: "2022-02-20 13:34:00"
tags:
categories:
description: >-
  mapping 是用来手动给 index 的字段 分配类型的，默认es会自动分配类型。 当你手动分配字段类型为 keyword 时，该字段不会分词存储，而是直接存储 PUT usertest { "mappings": { "properties": { "age":{ "type": "integ
---

<p>mapping 是用来手动给 index 的字段 分配类型的，默认es会自动分配类型。</p>
<p>当你手动分配字段类型为 keyword 时，该字段不会分词存储，而是直接存储</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">PUT usertest
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">integer</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">price</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">scaled_float</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">scaling_factor</span><span style="color: #800000;">"</span>: <span style="color: #800080;">100</span><span style="color: #000000;">
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>具体分词器，如下</p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202202/1680452-20220219210031915-216865256.png" alt="" width="432" height="190" loading="lazy" />&nbsp;</p>
<p>&nbsp;</p>
<p>可以为某个字段指定 分词器</p>
<div class="cnblogs_code">
<pre>PUT my-index-<span style="color: #800080;">000001</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">whitespace</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><a href="https://www.elastic.co/guide/en/elasticsearch/reference/7.17/specify-analyzer.html" target="_blank">不指定analyzer时，默认为以下顺序</a></p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202202/1680452-20220219205337566-1200729203.png" alt="" width="612" height="210" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202202/1680452-20220219212007195-1485785241.png" alt="" width="388" height="461" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>安装中文分词器 ik</h3>
<p>下载对应的版本</p>
<p><a href="https://github.com/medcl/elasticsearch-analysis-ik/releases" target="_blank">https://github.com/medcl/elasticsearch-analysis-ik/releases</a></p>
<p>&nbsp;</p>
<p>解压到plugins目录，命名为ik</p>
<p>&nbsp;</p>
<p>若是文件夹没有正常挂载出来，就直接复制进去</p>
<div class="cnblogs_code">
<pre>docker cp d:\elasticsearch\plugins\ik d7ea6aa5852a:/usr/share/elasticsearch/plugins</pre>
</div>
<p>&nbsp;</p>
<p>若是遇到 es 版本与 ik 版本不一致，直接修改ik版本</p>
<div class="cnblogs_code">
<pre>vi ./elasticsearch/ik/plugins/plugin-descriptor.properties</pre>
</div>
<p>&nbsp;</p>
<h3>开始使用 ik 分词</h3>
<p>手动检测这个词会怎样拆</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">中国科技大学</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ik_smart</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">中国科技大学</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ik_max_word</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 往往 ik_max_word 使用起来更好一点</span></pre>
</div>
<p>&nbsp;</p>
<p>手动设定 分词器 使用</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 手动设置 cn 的 name 字段的分词器
PUT cn 
{
</span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
  </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ik_max_word</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}  
}

# 使用
POST cn</span>/<span style="color: #000000;">_bulk
{</span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">cn</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">这是一个杯子</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">cn</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">中国博物馆</span><span style="color: #800000;">"</span>}<br /><br /># 验证是否成功<br />GET cn</pre>
</div>
<p>&nbsp;</p>
<p>除了指定存储时用什么分词器，还可以指定搜索时用什么分词器</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">PUT newcn 
{
</span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
  </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ik_max_word</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">search_analyzer</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">standard</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}  
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>做自己的分词器</h2>
<p>D:\elasticsearch\plugins\ik\config 里面建立自己的文件夹，如 otherword</p>
<p>&nbsp;</p>
<p>新建词库文件 aa.dic，里面放分词</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">vim aa.dic

瓦隆子
好对生素</span></pre>
</div>
<p>&nbsp;</p>
<p>新建&nbsp;extra_stopword.dic&nbsp;语气词库，用以忽略语气词</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">vim extra_stopword.dic

的
地
得</span></pre>
</div>
<p>&nbsp;</p>
<p>将新建的词库，写入配置文件</p>
<div class="cnblogs_code">
<pre>vim IKAnalyzer.cfg.xml</pre>
</div>
<div class="cnblogs_code">
<pre>&lt;?xml version=<span style="color: #800000;">"</span><span style="color: #800000;">1.0</span><span style="color: #800000;">"</span> encoding=<span style="color: #800000;">"</span><span style="color: #800000;">UTF-8</span><span style="color: #800000;">"</span>?&gt;
&lt;!DOCTYPE properties SYSTEM <span style="color: #800000;">"</span><span style="color: #800000;">http://java.sun.com/dtd/properties.dtd</span><span style="color: #800000;">"</span>&gt;
&lt;properties&gt;
    &lt;comment&gt;IK Analyzer 扩展配置&lt;/comment&gt;
    &lt;!--用户可以在这里配置自己的扩展字典 --&gt;
    &lt;entry key=<span style="color: #800000;">"</span><span style="color: #800000;">ext_dict</span><span style="color: #800000;">"</span>&gt;otherword/aa.dic&lt;/entry&gt;
     &lt;!--用户可以在这里配置自己的扩展停止词字典--&gt;
    &lt;entry key=<span style="color: #800000;">"</span><span style="color: #800000;">ext_stopwords</span><span style="color: #800000;">"</span>&gt;otherword/extra_stopword.dic&lt;/entry&gt;
    &lt;!--用户可以在这里配置远程扩展字典 --&gt;
    &lt;!-- &lt;entry key=<span style="color: #800000;">"</span><span style="color: #800000;">remote_ext_dict</span><span style="color: #800000;">"</span>&gt;words_location&lt;/entry&gt; --&gt;
    &lt;!--用户可以在这里配置远程扩展停止词字典--&gt;
    &lt;!-- &lt;entry key=<span style="color: #800000;">"</span><span style="color: #800000;">remote_ext_stopwords</span><span style="color: #800000;">"</span>&gt;words_location&lt;/entry&gt; --&gt;
&lt;/properties&gt;</pre>
</div>
<p>&nbsp;</p>
<p>重启完成</p>
<p>&nbsp;</p>
<p>测试使用</p>
<p><img src="https://img2022.cnblogs.com/blog/1680452/202202/1680452-20220220133405762-1608508058.png" alt="" width="1187" height="431" loading="lazy" /></p>
<p>&nbsp;</p>
