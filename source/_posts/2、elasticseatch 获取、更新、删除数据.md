---
title: "2、elasticseatch 获取、更新、删除数据"
date: "2022-02-18 22:50:00"
updated: "2022-02-19 17:00:00"
tags:
categories:
description: >-
  获取 简单获取 GET /user/_doc/1 // 获取user下id为1的数据 GET /user/_source/1 // 获取user下id为1的源数据 通过 url 查询数据 GET _search?q="明明" // 从所有的index中查找 GET user/_search?q=1
---

<h2>获取</h2>
<p>简单获取</p>
<div class="cnblogs_code">
<pre>GET /user/_doc/<span style="color: #800080;">1</span>
<span style="color: #008000;">//</span><span style="color: #008000;"> 获取user下id为1的数据</span>
<span style="color: #000000;">
GET </span>/user/_source/<span style="color: #800080;">1</span>
<span style="color: #008000;">//</span><span style="color: #008000;"> 获取user下id为1的源数据</span></pre>
</div>
<p>&nbsp;</p>
<p>通过 url 查询数据</p>
<div class="cnblogs_code">
<pre>GET _search?q=<span style="color: #800000;">"</span><span style="color: #800000;">明明</span><span style="color: #800000;">"</span>
<span style="color: #008000;">//</span><span style="color: #008000;"> 从所有的index中查找</span>
<span style="color: #000000;">
GET user</span>/_search?q=<span style="color: #800080;">1</span>
<span style="color: #008000;">//</span><span style="color: #008000;"> 从某个index中查找</span></pre>
</div>
<p>&nbsp;</p>
<h3>通过 request body 查询数据</h3>
<p>&nbsp;</p>
<h2>1、全文查询</h2>
<h4>match 查询</h4>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> match 为模糊查询，只要找到 keyword 里某个分词就能匹配到</span>
GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">明</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">from</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span><span style="color: #000000;">
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 查询 user下 name 字段带有 &ldquo;明&rdquo; 的数据 。从0开始，匹配一条</span></pre>
</div>
<p>&nbsp;</p>
<p>match 也可以做 fuzzy 模糊查询</p>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">zhong</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">fuzziness</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<h4>match_phrase 短语查询。</h4>
<p>结果中的 keyword 必须与 搜索的 keyword 必须连着，顺序也要保持一致</p>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match_phrase</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ha ha</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<h4>&nbsp;multi_match 多字段查询</h4>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">multi_match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">imname</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">address</span><span style="color: #800000;">"</span><span style="color: #000000;">]
    }
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 在name和address中查询</span>
<span style="color: #000000;">
GET user</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">multi_match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">imname</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">address^2</span><span style="color: #800000;">"</span><span style="color: #000000;">]
    }
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 给address权重*2，这样排序就会更靠前</span></pre>
</div>
<p>&nbsp;</p>
<h4>query string （类似match，但是match必须指定字段名）</h4>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">query_string</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">default_field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>, <span style="color: #008000;">//</span><span style="color: #008000;"> 可以选择是否指定字段名，不指定就索引全部</span>
      <span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">明 OR 1</span><span style="color: #800000;">"</span> <span style="color: #008000;">//</span><span style="color: #008000;"> keyword可以 用 AND OR 等字段</span>
<span style="color: #000000;">    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<h4>match_all 查询某个index下所有数据</h4>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 查询 user 下所有的数据</span></pre>
</div>
<p>&nbsp;</p>
<h2>2、term 级别查询</h2>
<h4>term 查询</h4>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">I am value</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> term级别查询，是直接查询，不做分词，不会大小写转换。
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 若是存储时是按照分词存储的话，直接查是查不到的

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 注：分词存储的时候，默认所有分词都会转为小写</span></pre>
</div>
<p>&nbsp;</p>
<h4>range 查询</h4>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">gte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">lte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">30</span><span style="color: #000000;">
      }
    }
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 查询age字段，&gt;=20岁，&lt;=30岁</span></pre>
</div>
<p>&nbsp;</p>
<h4>exists 查询</h4>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">exists</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 查询带有name字段的数据</span></pre>
</div>
<p>&nbsp;</p>
<h4>fuzzy 模糊查询</h4>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fuzzy</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">zhong</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 即便 zhang 输成 zhong 也能找到 zhang 的数据</span></pre>
</div>
<p>&nbsp;</p>
<h2>3、复合查询</h2>
<p>must：必须匹配，查询上下文，加分</p>
<p>should：应该匹配，查询上下文，加分</p>
<p>must_not：必须不匹配，过滤上下文，过滤</p>
<p>filter：必须匹配，过滤上下文，过滤</p>
<div class="cnblogs_code">
<pre>GET user/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">bool</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">must</span><span style="color: #800000;">"</span>: [ <span style="color: #008000;">//</span><span style="color: #008000;"> state 必须=tn</span>
<span style="color: #000000;">        {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">state</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">tn</span><span style="color: #800000;">"</span><span style="color: #000000;">
            }
          }
        }
      ],
      </span><span style="color: #800000;">"</span><span style="color: #800000;">must_not</span><span style="color: #800000;">"</span>: [  <span style="color: #008000;">//</span><span style="color: #008000;"> gender 必须不能为m</span>
<span style="color: #000000;">        {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">m</span><span style="color: #800000;">"</span><span style="color: #000000;">
            }
          }
        }
      ],
      </span><span style="color: #800000;">"</span><span style="color: #800000;">should</span><span style="color: #800000;">"</span>: [ <span style="color: #008000;">//</span><span style="color: #008000;"> name应该有1</span>
<span style="color: #000000;">        {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      ],
      </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span>: [ <span style="color: #008000;">//</span><span style="color: #008000;"> age必须&gt;=10，&lt;=30</span>
<span style="color: #000000;">        {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">gte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">10</span><span style="color: #000000;">,
              </span><span style="color: #800000;">"</span><span style="color: #800000;">lte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">30</span><span style="color: #000000;">
            }
          }
        }
      ]
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<h2>更新</h2>
<p>post 和 put</p>
<div class="cnblogs_code">
<pre>POST user/_doc/<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">看看</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

PUT user</span>/_doc/<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">看看</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> post 和 put 都会删除原有数据后，再进行插入。
</span><span style="color: #008000;">//</span><span style="color: #008000;"> version 和 seq_no 都会更新</span></pre>
</div>
<p>&nbsp;</p>
<p>post 的 _update 更新</p>
<div class="cnblogs_code">
<pre>POST user/_update/<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">doc</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">看看</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 会在原有数据上进行增加更新
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 若是里面已经存在该键值对，则不会更新，version 和 seq_no 也不会更新</span></pre>
</div>
<p>&nbsp;</p>
<h2>删除</h2>
<div class="cnblogs_code">
<pre>DELETE user/_doc/<span style="color: #800080;">1</span>
<span style="color: #008000;">//</span><span style="color: #008000;"> 删除 index 下某条数据</span>
<span style="color: #000000;">
DELETE user
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除整个user</span></pre>
</div>
<p>&nbsp;</p>
<h2>批量插入</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">POST _bulk
{</span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">66</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">key</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">661</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">key</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 或者</span>
<span style="color: #000000;">
POST _bulk
{</span><span style="color: #800000;">"</span><span style="color: #800000;">create</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">67</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">value1</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">create</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">671</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">value1</span><span style="color: #800000;">"</span>}</pre>
</div>
<p>&nbsp;</p>
<h2>批量删除</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">POST _bulk
{</span><span style="color: #800000;">"</span><span style="color: #800000;">delete</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">661</span><span style="color: #800000;">"</span>}}</pre>
</div>
<p>&nbsp;</p>
<h2>批量更新</h2>
<div class="cnblogs_code">
<pre><span style="color: #000000;">POST _bulk
{</span><span style="color: #800000;">"</span><span style="color: #800000;">update</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">doc</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">小明</span><span style="color: #800000;">"</span>}}</pre>
</div>
<p>&nbsp;</p>
