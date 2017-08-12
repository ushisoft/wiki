# 安装

### 配置文件

[官方示例](https://www.elastic.co/guide/en/logstash/current/config-examples.html)

### Elasticsearch安装

#### 通过Docker运行

下载镜像

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:5.5.1
```

从官方下载

```
docker pull elasticsearch
```

运行

```
docker run -p 9200:9200 -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" docker.elastic.co/elasticsearch/elasticsearch:5.5.1
```



### Kibana安装

#### 通过Docker运行

下载

```
docker pull docker.elastic.co/kibana/kibana:5.5.1
```

从官方下载

```
docker pull kibana
```

运行

