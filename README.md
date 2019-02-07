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
