# elasticsearch部署相关业务

## 概述

elasticsearch是一个开源分析引擎. 可以作为简易的搜索引擎使用.

## 部署流程

```
docker pull elasticsearch (注意: 5.6以后, 这个镜像只在该官网更新)
docker run -d -p 9200:9200 -p 9300:9300 -v /home/glrh11/workspace/esdata:/usr/share/elasticsearch/data --env ES_JAVA_OPTS="-Xms512m -Xmx512m" --name kitty-elastic elasticsearch 

docker run -d -p 9200:9200 -p 9300:9300 -v /home/centos/workspace/elasticdata:/usr/share/elasticsearch/data --env ES_JAVA_OPTS="-Xms512m -Xmx512m" --name kitty-elastic elasticsearch 
```

## F&Q

### 内存不足的错误
There is insufficient memory for the Java Runtime Environment to continue.

因为5.X版本默认以2GB内存启动, 所以需要修改配置项目: 
`https://stackoverflow.com/questions/29447434/elasticsearch-memory-probles`
`https://www.elastic.co/guide/en/elasticsearch/reference/5.2/docker.html`
`https://www.elastic.co/guide/en/elasticsearch/reference/master/heap-size.html`

`改变这个配置文件:/etc/elasticsearch/jvm.options 这两个配置: -Xms512m -Xmx512m`

修改方法: 带上这个环境变量 `ES_JAVA_OPTS=-Xms512m -Xmx512m`

### elastic太耗内存了...怎么办

建立swap, 限制-Xms512m -Xmx512m 到90m; 
限制整个docker的运行内存不靠谱, 容易导致异常退出.
