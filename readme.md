Pre-req:
java 
zookeeper


yum install java 
java -version
-------------------------------
zookeeper:
wget http://mirrors.estointernet.in/apache/zookeeper/stable/zookeeper-3.4.12.tar.gz
cd /opt
tar xvzf zookeeper-3.4.12.tar.gz -C /opt/
cd zookeeper-3.4.12
mkdir data
/conf/zoo.cfg  edit this with below values, if no zoo.cfg, use sample file and create zoo.cfg 

tickTime = 2000
dataDir = /opt/zookeeper-3.4.12/data
clientPort = 2181
initLimit = 5
syncLimit = 2

cd /bin 
./zkServer.sh start
./zkCli.sh  (output like below)

WATCHER::
WatchedEvent state:SyncConnected type:None path:null
------------------------------

useradd kafka
passwd kafka
visudo 
kafka 

wget http://www-eu.apache.org/dist/kafka/2.1.0/kafka_2.11-2.1.0.tgz

mkdir /opt/kafka
cd /opt/kafka
tar -xvzf kafka_2.11-2.1.0.tgz

start the kafka service:
/opt/kafka/kafka_2.11-2.1.0/bin/kafka-server-start.sh /opt/kafka/kafka_2.11-2.1.0/config/server.properties

to run backgroup 
nohup /opt/kafka/kafka_2.11-2.1.0/bin/kafka-server-start.sh /opt/kafka/kafka_2.11-2.1.0/config/server.properties 2>&1 &


testing
/opt/kafka/kafka_2.11-2.1.0/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1  --partitions 1 --topic testing
You should see the following output:
Created topic "testing".

Now, ask Zookeeper to list available topics on Apache Kafka by running the following command:
/opt/kafka/kafka_2.11-2.1.0/bin/kafka-topics.sh --list --zookeeper localhost:2181
You should see the following output:
testing

Now, publish a sample messages to Apache Kafka topic called testing by using the following producer command:
/opt/kafka/kafka_2.11-2.1.0/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic testing
After running above command, enter some messages like "Hi how are you?" press enter, then enter another message like "Where are you?"

Now, use consumer command to check for messages on Apache Kafka Topic called testing by running the following command:
/opt/kafka/kafka_2.11-2.1.0/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic testing --from-beginning
You should see the following output:

Heyy this  testing..!
Where are you?
