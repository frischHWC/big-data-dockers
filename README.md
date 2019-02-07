# Big Data Dockers

This projects aims to provide some full, distributed, easy-to-use and launch dockers on different Big Data technologies.
Once your dockers are launched, you can easily connect to them and test whatever you want on them ! 
(e.g. Try some requests, check what's happening on the file system in some cases, try your code etc...)  


## docker-hbase

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


Docker are based on (this dockers from gitHub)[https://github.com/big-data-europe/docker-hbase] 

