---
title: "4、go 中使用 elasticsearch"
date: "2022-02-20 17:13:00"
tags:
categories:
description: >-
  package main import ( "context" "encoding/json" "fmt" "github.com/olivere/elastic/v7" "log" "os" "reflect" ) type User struct { Name string `json:"nam
---

<div class="cnblogs_code">
<pre><span style="color: #000000;">package main

import (
    </span><span style="color: #800000;">"</span><span style="color: #800000;">context</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">encoding/json</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">fmt</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">github.com/olivere/elastic/v7</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">log</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">os</span><span style="color: #800000;">"</span>
    <span style="color: #800000;">"</span><span style="color: #800000;">reflect</span><span style="color: #800000;">"</span><span style="color: #000000;">
)

type User </span><span style="color: #0000ff;">struct</span><span style="color: #000000;"> {
    Name </span><span style="color: #0000ff;">string</span> `json:<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">`
    Age  </span><span style="color: #0000ff;">uint</span>   `json:<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">`
}

</span><span style="color: #0000ff;">const</span> mapping =<span style="color: #000000;"> `
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
                </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">ik_max_word</span><span style="color: #800000;">"</span><span style="color: #000000;">
                },
                </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">long</span><span style="color: #800000;">"</span><span style="color: #000000;">
                }
            }
        }
    }
}`

func main() {
    url :</span>= <span style="color: #800000;">"</span><span style="color: #800000;">http://172.31.224.1:9200/</span><span style="color: #800000;">"</span><span style="color: #000000;">

    ctx :</span>=<span style="color: #000000;"> context.Background()

    logger :</span>= log.New(os.Stdout, <span style="color: #800000;">"</span><span style="color: #800000;">看看</span><span style="color: #800000;">"</span><span style="color: #000000;">, log.LstdFlags)

    </span><span style="color: #008000;">//</span><span style="color: #008000;">elastic.SetSniff(false)，防止elastic对ip进行转变</span>
    client, err := elastic.NewClient(elastic.SetURL(url), elastic.SetSniff(<span style="color: #0000ff;">false</span><span style="color: #000000;">), elastic.SetTraceLog(logger))
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ping es数据库，查看是否ping通，并获取 es 版本号</span>
    info, code, err :=<span style="color: #000000;"> client.Ping(url).Do(ctx)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Elasticsearch returned with code %d and version %s\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, code, info.Version.Number)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 直接获取 es 版本号</span>
    esversion, err :=<span style="color: #000000;"> client.ElasticsearchVersion(url)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Elasticsearch version %s\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, esversion)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 查看 user 是否存在</span>
    exists, err := client.IndexExists(<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">).Do(ctx)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">user索引是否存在 %t \n</span><span style="color: #800000;">"</span><span style="color: #000000;">, exists)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 若不存在就创建</span>
    <span style="color: #0000ff;">if</span> !<span style="color: #000000;">exists {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建 user 索引</span>
        createIndex, err := client.CreateIndex(<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">).BodyString(mapping).Do(ctx)
        </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">            panic(err)
        }
        </span><span style="color: #0000ff;">if</span> !<span style="color: #000000;">createIndex.Acknowledged {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Not acknowledged</span>
<span style="color: #000000;">        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> post 方式 给 user 添加数据</span>
    user1 := User{Name: <span style="color: #800000;">"</span><span style="color: #800000;">新名字</span><span style="color: #800000;">"</span>, Age: <span style="color: #800080;">99</span><span style="color: #000000;">}
    put1, err :</span>=<span style="color: #000000;"> client.Index().
        Index(</span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">).
        BodyJson(user1).
        Do(ctx)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Indexed user %s to index %s, type %s\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, put1.Id, put1.Index, put1.Type)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 刷新确保文件被写入</span>
    _, err = client.Flush().Index(<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">).Do(ctx)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        panic(err)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 获取某条数据</span>
    get1, err :=<span style="color: #000000;"> client.Get().
        Index(</span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">).
        Id(</span><span style="color: #800000;">"</span><span style="color: #800000;">4QTnFX8BjicySfgw5Njd</span><span style="color: #800000;">"</span><span style="color: #000000;">).
        Do(ctx)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> get1.Found {
        fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got document %s in version %d from index %s, type %s\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, get1.Id, get1.Version, get1.Index, get1.Type)
        fmt.Println(</span><span style="color: #0000ff;">string</span>(get1.Source)) <span style="color: #008000;">//</span><span style="color: #008000;"> 字符串数据</span>
        u :=<span style="color: #000000;"> User{}
        json.Unmarshal(get1.Source, </span>&amp;u) <span style="color: #008000;">//</span><span style="color: #008000;"> 将byte转为struct</span>
<span style="color: #000000;">        fmt.Println(u)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> term 级别的查询</span>
    termQuery := elastic.NewTermQuery(<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">99</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    searchResult, err :</span>=<span style="color: #000000;"> client.Search().
        Index(</span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">).
        Query(termQuery).
        </span><span style="color: #008000;">//</span><span style="color: #008000;">Sort("age", true). </span><span style="color: #008000;">//</span><span style="color: #008000;"> sort by "age" field, ascending
        </span><span style="color: #008000;">//</span><span style="color: #008000;">From(0).Size(10).   </span><span style="color: #008000;">//</span><span style="color: #008000;"> take documents 0-9</span>
        Pretty(<span style="color: #0000ff;">true</span>). <span style="color: #008000;">//</span><span style="color: #008000;"> pretty print request and response JSON</span>
        Do(ctx)       <span style="color: #008000;">//</span><span style="color: #008000;"> execute</span>
    <span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Query took %d milliseconds\n</span><span style="color: #800000;">"</span>, searchResult.TookInMillis) <span style="color: #008000;">//</span><span style="color: #008000;"> 查询耗时x毫秒

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将结果，循环打印出来</span>
    <span style="color: #0000ff;">var</span><span style="color: #000000;"> ttyp User
    </span><span style="color: #0000ff;">for</span> _, item :=<span style="color: #000000;"> range searchResult.Each(reflect.TypeOf(ttyp)) {
        </span><span style="color: #0000ff;">if</span> t, ok :=<span style="color: #000000;"> item.(User); ok {
            fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">User by %s: %d\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, t.Name, t.Age)
        }
    }

    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Found a total of %d user\n</span><span style="color: #800000;">"</span>, searchResult.TotalHits()) <span style="color: #008000;">//</span><span style="color: #008000;"> 一共 xx 条</span>

    <span style="color: #008000;">/*</span><span style="color: #008000;">**********************************************************************************</span><span style="color: #008000;">*/</span>

    <span style="color: #008000;">//</span><span style="color: #008000;"> Here's how you iterate through results with full control over each step.</span>
    <span style="color: #0000ff;">if</span> searchResult.Hits.TotalHits &gt; <span style="color: #800080;">0</span><span style="color: #000000;"> {
        fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">Found a total of %d tweets\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, searchResult.Hits.TotalHits)

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Iterate through results</span>
        <span style="color: #0000ff;">for</span> _, hit :=<span style="color: #000000;"> range searchResult.Hits.Hits {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> hit.Index contains the name of the index

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Deserialize hit.Source into a Tweet (could also be just a map[string]interface{}).</span>
            <span style="color: #0000ff;">var</span><span style="color: #000000;"> t Tweet
            err :</span>= json.Unmarshal(*hit.Source, &amp;<span style="color: #000000;">t)
            </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Deserialization failed</span>
<span style="color: #000000;">            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Work with tweet</span>
            fmt.Printf(<span style="color: #800000;">"</span><span style="color: #800000;">Tweet by %s: %s\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, t.User, t.Message)
        }
    } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> No hits</span>
        fmt.Print(<span style="color: #800000;">"</span><span style="color: #800000;">Found no tweets\n</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Update a tweet by the update API of Elasticsearch.
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> We just increment the number of retweets.</span>
    update, err := client.Update().Index(<span style="color: #800000;">"</span><span style="color: #800000;">twitter</span><span style="color: #800000;">"</span>).Type(<span style="color: #800000;">"</span><span style="color: #800000;">tweet</span><span style="color: #800000;">"</span>).Id(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">).
        Script(elastic.NewScriptInline(</span><span style="color: #800000;">"</span><span style="color: #800000;">ctx._source.retweets += params.num</span><span style="color: #800000;">"</span>).Lang(<span style="color: #800000;">"</span><span style="color: #800000;">painless</span><span style="color: #800000;">"</span>).Param(<span style="color: #800000;">"</span><span style="color: #800000;">num</span><span style="color: #800000;">"</span>, <span style="color: #800080;">1</span><span style="color: #000000;">)).
        Upsert(map[</span><span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">interface</span>{}{<span style="color: #800000;">"</span><span style="color: #800000;">retweets</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">}).
        Do(ctx)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    fmt.Printf(</span><span style="color: #800000;">"</span><span style="color: #800000;">New version of tweet %q is now %d\n</span><span style="color: #800000;">"</span><span style="color: #000000;">, update.Id, update.Version)

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Delete an index.</span>
    deleteIndex, err := client.DeleteIndex(<span style="color: #800000;">"</span><span style="color: #800000;">twitter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Do(ctx)
    </span><span style="color: #0000ff;">if</span> err !=<span style="color: #000000;"> nil {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Handle error</span>
<span style="color: #000000;">        panic(err)
    }
    </span><span style="color: #0000ff;">if</span> !<span style="color: #000000;">deleteIndex.Acknowledged {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> Not acknowledged</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
