# 实践

在通往最佳实践的路上。

### Logstash

#### 配置

官方示例：[examples](https://www.elastic.co/guide/en/logstash/current/config-examples.html)

#### Filter

##### grok

日志分析插件。

有个很好用的格式配置调试站点：[herokuapp](http://grokdebug.herokuapp.com/)

官方定义的样式参考：[logstash-patterns-core](https://github.com/logstash-plugins/logstash-patterns-core/tree/master/patterns)

##### date

需配合grok使用

##### mutate

对Field进行操作，参考[docs](https://www.elastic.co/guide/en/logstash/current/plugins-filters-mutate.html)



### Elasticsearch

#### 查询

参考[官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/5.5/query-dsl-query-string-query.html)

特别值得留意的是几个保留字符，都是有特殊含义的：

```
+ - = && || > < ! ( ) { } [ ] ^ " ~ * ? : \ /
```