# Big Data Dockers

This projects aims to provide some full, distributed, easy-to-use and launch dockers on different Big Data technologies.
Once your dockers are launched, you can easily connect to them and test whatever you want on them ! 
(e.g. Try some requests, check what's happening on the file system in some cases, try your code etc...)  


## HBase

HBase 1.2.6

To launch hbase docker :
Go to folder `docker-hbase` and run : 
```
docker-compose up -d
```

If everything went well : 
```
HW15215:docker-hbase frisch$ docker ps -a
CONTAINER ID        IMAGE                                                    COMMAND                  CREATED             STATUS                    PORTS                                            NAMES
c3f1764cc561        bde2020/hbase-regionserver:1.0.0-hbase1.2.6              "/entrypoint.sh /run…"   19 minutes ago      Up 18 minutes             16020/tcp, 16030/tcp, 0.0.0.0:16031->16031/tcp   hbase-regionserver-1
248c867a9c5d        bde2020/hbase-regionserver:1.0.0-hbase1.2.6              "/entrypoint.sh /run…"   28 minutes ago      Up 28 minutes             16020/tcp, 0.0.0.0:16030->16030/tcp              hbase-regionserver
10f6cee46bfe        bde2020/hbase-master:1.0.0-hbase1.2.6                    "/entrypoint.sh /run…"   28 minutes ago      Up 28 minutes             16000/tcp, 0.0.0.0:16010->16010/tcp              hbase-master
969935013a83        bde2020/hadoop-nodemanager:2.0.0-hadoop2.7.4-java8       "/entrypoint.sh /run…"   34 minutes ago      Up 34 minutes (healthy)   0.0.0.0:8042->8042/tcp                           hbase-nodemanager
2027dc68c353        bde2020/hadoop-resourcemanager:2.0.0-hadoop2.7.4-java8   "/entrypoint.sh /run…"   34 minutes ago      Up 34 minutes (healthy)   0.0.0.0:8088->8088/tcp                           hbase-resourcemanager
273b0570f0eb        bde2020/hadoop-datanode:2.0.0-hadoop2.7.4-java8          "/entrypoint.sh /run…"   34 minutes ago      Up 34 minutes (healthy)   0.0.0.0:50075->50075/tcp                         hbase-datanode
d7c18192ffde        bde2020/hadoop-historyserver:2.0.0-hadoop2.7.4-java8     "/entrypoint.sh /run…"   34 minutes ago      Up 34 minutes (healthy)   0.0.0.0:8188->8188/tcp                           hbase-historyserver
f029a8089993        zookeeper:3.4.10                                         "/docker-entrypoint.…"   34 minutes ago      Up 34 minutes             2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp       hbase-zookeeper
09bffa3a711b        bde2020/hadoop-namenode:2.0.0-hadoop2.7.4-java8          "/entrypoint.sh /run…"   34 minutes ago      Up 34 minutes (healthy)   0.0.0.0:50070->50070/tcp                         hbase-namenode
```

You can start a HBase shell with this command : 

```
HW15215:docker-hbase frisch$ docker exec -it hbase-master hbase shell
2019-02-07 10:10:19,021 WARN  [main] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
HBase Shell; enter 'help<RETURN>' for list of supported commands.
Type "exit<RETURN>" to leave the HBase Shell
Version 1.2.6, rUnknown, Mon May 29 02:25:32 CDT 2017

hbase(main):001:0> 
```


Docker are based on [this dockers from gitHub](https://github.com/big-data-europe/docker-hbase)


## Spark

Spark-2.4.0

To launch hbase docker :
Go to folder `docker-spark` and run : 
```
docker-compose up -d
```

If everything went well : 
```
HW15215:docker-spark frisch$ docker ps -a
CONTAINER ID        IMAGE                                COMMAND                  CREATED             STATUS              PORTS                                                                                                           NAMES
64f687f476ee        gettyimages/spark:2.4.0-hadoop-3.0   "bin/spark-class org…"   4 seconds ago       Up 3 seconds        7012-7015/tcp, 8883/tcp, 0.0.0.0:8083->8083/tcp                                                                 docker-spark_worker3_1
fc13367829be        gettyimages/spark:2.4.0-hadoop-3.0   "bin/spark-class org…"   4 seconds ago       Up 3 seconds        7012-7015/tcp, 8884/tcp, 0.0.0.0:8084->8084/tcp                                                                 docker-spark_worker4_1
1373973686e7        gettyimages/spark:2.4.0-hadoop-3.0   "bin/spark-class org…"   4 minutes ago       Up 4 minutes        7012-7015/tcp, 8881/tcp, 0.0.0.0:8081->8081/tcp                                                                 docker-spark_worker1_1
44279f43fb73        gettyimages/spark:2.4.0-hadoop-3.0   "bin/spark-class org…"   4 minutes ago       Up 4 minutes        7012-7015/tcp, 8882/tcp, 0.0.0.0:8082->8082/tcp                                                                 docker-spark_worker2_1
80a4bd3964ce        gettyimages/spark:2.4.0-hadoop-3.0   "bin/spark-class org…"   4 minutes ago       Up 4 minutes        0.0.0.0:4040->4040/tcp, 0.0.0.0:6066->6066/tcp, 0.0.0.0:7077->7077/tcp, 0.0.0.0:8080->8080/tcp, 7001-7005/tcp   docker-spark_master_1
```

You can start a Spark scala shell :

```
HW15215:docker-spark frisch$ docker exec -it docker-spark_worker2_1 spark-shell
2019-02-07 10:53:25 WARN  NativeCodeLoader:60 - Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
Spark context Web UI available at http://localhost:4040
Spark context available as 'sc' (master = local[*], app id = local-1549536814297).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.4.0
      /_/
         
Using Scala version 2.11.12 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_202)
Type in expressions to have them evaluated.
Type :help for more information.

scala> 
```

N.B : You should also see spark master and its worker at this url : [http://localhost:8080](http://localhost:8080)

Dockers are base on [this docker](https://hub.docker.com/r/gettyimages/spark/tags)

## Hive

Hive 2

To launch hive docker :
Go to folder `docker-hive` and run : 
```
docker-compose up -d
```

If everything went well : 
```
HW15215:docker-hive frisch$ docker ps -a
CONTAINER ID        IMAGE                                             COMMAND                  CREATED             STATUS                   PORTS                                          NAMES
82677e8b32ca        bde2020/hive:2.3.2-postgresql-metastore           "entrypoint.sh /opt/…"   5 minutes ago       Up 5 minutes             10000/tcp, 0.0.0.0:9083->9083/tcp, 10002/tcp   docker-hive_hive-metastore_1
faf01f803a74        bde2020/hadoop-datanode:2.0.0-hadoop2.7.4-java8   "/entrypoint.sh /run…"   5 minutes ago       Up 5 minutes (healthy)   0.0.0.0:50075->50075/tcp                       docker-hive_datanode_1
7827ca2d566e        bde2020/hadoop-namenode:2.0.0-hadoop2.7.4-java8   "/entrypoint.sh /run…"   5 minutes ago       Up 5 minutes (healthy)   0.0.0.0:50070->50070/tcp                       docker-hive_namenode_1
8d43c38fec0e        bde2020/hive:2.3.2-postgresql-metastore           "entrypoint.sh /bin/…"   5 minutes ago       Up 5 minutes             0.0.0.0:10000->10000/tcp, 10002/tcp            docker-hive_hive-server_1
```

You can start a hive shell with this command : 

```
HW15215:docker-hive frisch$ docker exec -it docker-hive_hive-server_1 hive
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/hive/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/hadoop-2.7.4/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]

Logging initialized using configuration in file:/opt/hive/conf/hive-log4j2.properties Async: true
Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
hive> 
```

Docker are based on [this dockers from gitHub](https://github.com/big-data-europe/docker-hive)


## Kafka



To launch hive docker :
Go to folder `docker-kafka` and run : 
```
docker-compose up -d
```

If everything went well : 
```
HW15215:docker-kafka frisch$ docker ps -a
CONTAINER ID        IMAGE                                             COMMAND                  CREATED              STATUS              PORTS                                                        NAMES
3ae741b345b2        confluentinc/cp-enterprise-control-center:5.1.0   "/etc/confluent/dock…"   About a minute ago   Up About a minute   0.0.0.0:9021->9021/tcp                                       docker-kafka_control-center_1
e390aadf9918        confluentinc/cp-kafka-rest:5.1.0                  "/etc/confluent/dock…"   About a minute ago   Up About a minute   0.0.0.0:8082->8082/tcp                                       docker-kafka_rest-proxy_1
d23bdd30f518        confluentinc/cp-schema-registry:5.1.0             "/etc/confluent/dock…"   About a minute ago   Up About a minute   0.0.0.0:8081->8081/tcp                                       docker-kafka_schema-registry_1
779c770d807c        confluentinc/cp-enterprise-kafka:5.1.0            "/etc/confluent/dock…"   About a minute ago   Up About a minute   0.0.0.0:9092->9092/tcp, 0.0.0.0:29092->29092/tcp             docker-kafka_broker1_1
b9e269a23e4c        confluentinc/cp-enterprise-kafka:5.1.0            "/etc/confluent/dock…"   About a minute ago   Up About a minute   0.0.0.0:9093->9093/tcp, 9092/tcp, 0.0.0.0:29093->29093/tcp   docker-kafka_broker2_1
fe72c757d745        confluentinc/cp-zookeeper:5.1.0                   "/etc/confluent/dock…"   About a minute ago   Up About a minute   2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp                   docker-kafka_zookeeper_1
```

You can log on a kafka broker and launch some commands, like this :

```
HW15215:docker-kafka frisch$ docker exec -it docker-kafka_broker_1 bash
root@broker:/# kafka-topics --zookeeper zookeeper:2181 --list
__confluent.support.metrics
__consumer_offsets
_confluent-command
_confluent-controlcenter-5-1-0-1-AlertHistoryStore-changelog
_confluent-controlcenter-5-1-0-1-Group-ONE_MINUTE-changelog
_confluent-controlcenter-5-1-0-1-Group-THREE_HOURS-changelog
_confluent-controlcenter-5-1-0-1-KSTREAM-OUTEROTHER-0000000096-store-changelog
_confluent-controlcenter-5-1-0-1-KSTREAM-OUTERTHIS-0000000095-store-changelog
_confluent-controlcenter-5-1-0-1-MetricsAggregateStore-changelog
_confluent-controlcenter-5-1-0-1-MetricsAggregateStore-repartition
_confluent-controlcenter-5-1-0-1-MonitoringMessageAggregatorWindows-ONE_MINUTE-changelog
_confluent-controlcenter-5-1-0-1-MonitoringMessageAggregatorWindows-THREE_HOURS-changelog
_confluent-controlcenter-5-1-0-1-MonitoringStream-ONE_MINUTE-changelog
_confluent-controlcenter-5-1-0-1-MonitoringStream-THREE_HOURS-changelog
_confluent-controlcenter-5-1-0-1-MonitoringTriggerStore-changelog
_confluent-controlcenter-5-1-0-1-MonitoringVerifierStore-changelog
_confluent-controlcenter-5-1-0-1-TriggerActionsStore-changelog
_confluent-controlcenter-5-1-0-1-TriggerEventsStore-changelog
_confluent-controlcenter-5-1-0-1-actual-group-consumption-rekey
_confluent-controlcenter-5-1-0-1-aggregate-topic-partition
_confluent-controlcenter-5-1-0-1-aggregate-topic-partition-changelog
_confluent-controlcenter-5-1-0-1-aggregatedTopicPartitionTableWindows-ONE_MINUTE-changelog
_confluent-controlcenter-5-1-0-1-aggregatedTopicPartitionTableWindows-THREE_HOURS-changelog
_confluent-controlcenter-5-1-0-1-cluster-rekey
_confluent-controlcenter-5-1-0-1-error-topic
_confluent-controlcenter-5-1-0-1-expected-group-consumption-rekey
_confluent-controlcenter-5-1-0-1-group-aggregate-topic-ONE_MINUTE
_confluent-controlcenter-5-1-0-1-group-aggregate-topic-ONE_MINUTE-changelog
_confluent-controlcenter-5-1-0-1-group-aggregate-topic-THREE_HOURS
_confluent-controlcenter-5-1-0-1-group-aggregate-topic-THREE_HOURS-changelog
_confluent-controlcenter-5-1-0-1-group-stream-extension-rekey
_confluent-controlcenter-5-1-0-1-metrics-trigger-measurement-rekey
_confluent-controlcenter-5-1-0-1-monitoring-aggregate-rekey
_confluent-controlcenter-5-1-0-1-monitoring-aggregate-rekey-changelog
_confluent-controlcenter-5-1-0-1-monitoring-message-rekey
_confluent-controlcenter-5-1-0-1-monitoring-trigger-event-rekey
_confluent-metrics
_confluent-monitoring
_schemas
```

Docker are based on [this dockers from Confluent](https://github.com/confluentinc/cp-docker-images)

