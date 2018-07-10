
**docker + elasticsearch + logstash + kibana**


使用
----

1. 安装 `docker` 和 `docker-compose`
2. git clone 代码到本地
    ```
    $ git clone git@github.com:Gekkoou/docker-elk.git
    ```
3. 执行命令 (Ubuntu为例)
    ```
    $ cd docker-elk
    $ sudo sysctl -w vm.max_map_count=262144
    $ sudo chmod 777 log
    $ sudo chmod 777 ./logstash/logs
    $ sudo chmod 777 ./logstash/data
    $ docker-compose up -d
    ```

打开 `chrome` 插件 `ElasticSearch Head` 查看详情, 或浏览器访问 `localhost:5601` 进入 `Kibana` 界面进行操作

本例子通过 `logstash` 读取 `nginx_access.log` 日志, 过滤后输出到 `elasticsearch`
可自行更改 `logstash/config/logstash-nginx.conf` 代码和 `docker-compose.yml` 中 `logstash` 的 `command` 命令

目录结构
----

```
├── elasticsearch                      elasticsearch目录
│   └── es                             es目录
│       │── config                     es配置目录
│       │   │── elasticsearch.yml      es配置文件
│       │   │── jvm.options            es配置文件
│       │   └── log4j2.properties      es配置文件
│       │── data                       data目录
│       │── logs                       logs目录
│       └── plugins                    plugins目录
│           └── ik                     ik分词
│── log                                log目录
│   └── nginx_access.log               nginx日志(测试用)
│── logstash                           logstash目录
│   │── config                         logstash配置目录
│   │   │── log4j2.properties          logstash配置文件
│   │   │── logstash.yml               logstash配置文件
│   │   └── logstash-nginx.conf        logstash配置文件
│   │── data                           data目录
│   └── logs                           logs目录
└── docker-compose.yml                 docker-compose配置文件
```

es集群
----

`elasticsearch` 目录下存有 `es1` `es2` 目录, 可开启集群

`docker-compose.yml` 去除 `es1` `es2` 相关注释

`elasticsearch/es/config/elasticsearch.yml` 去除注释

`docker-compose up -d` 启动

`es` 与 `es1` 为 `master` 节点, `es2` 为 `data` 节点
