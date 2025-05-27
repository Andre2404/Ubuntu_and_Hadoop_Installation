# Ubuntu_and_Hadoop_Installation
cara install hadoop di linux dan konfigurasi

Install Java JDK 11 di Semua Node

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
java -version
```

Tambahkan User Hadoop (Opsional)

```bash
sudo adduser hadoop
sudo usermod -aG sudo hadoop
```

Login sebagai user hadoop:
```bash
su - hadoop
```

Setup SSH Tanpa Password (di Master)

```bash
ssh-keygen -t rsa -P ""
ssh-copy-id hadoop@slave1_ip
ssh-copy-id hadoop@slave2_ip
```

Tes SSH tanpa password:

```bash
ssh hadoop@slave1_ip
ssh hadoop@slave2_ip
```

Download dan Ekstrak Hadoop 3.3.6 di Semua Node

```bash
wget https://archive.apache.org/dist/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz
tar -xvf hadoop-3.3.6.tar.gz
sudo mv hadoop-3.3.6 /usr/local/hadoop
```

Konfigurasi Hadoop Environment

```bash
nano ~/.bashrc
```
Tambahkan:
```bash
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```
```bash
source ~/.bashrc
```

# Edit Konfigurasi Hadoop (di Master)
core-site.xml
```bash
nano $HADOOP_HOME/etc/hadoop/core-site.xml
```
Tambahkan:
```bash
<configuration>
 <property>
   <name>fs.defaultFS</name>
   <value>hdfs://master_ip:9000</value>
 </property>
</configuration>
```
hdfs-site.xml
```bash
nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml
```
Tambahkan:
```bash
<configuration>
 <property>
   <name>dfs.replication</name>
   <value>2</value>
 </property>
 <property>
   <name>dfs.namenode.name.dir</name>
   <value>file:///usr/local/hadoop/hadoop_data/hdfs/namenode</value>
 </property>
 <property>
   <name>dfs.datanode.data.dir</name>
   <value>file:///usr/local/hadoop/hadoop_data/hdfs/datanode</value>
 </property>
</configuration>
```
mapred-site.xml
```bash
cp $HADOOP_HOME/etc/hadoop/mapred-site.xml.template $HADOOP_HOME/etc/hadoop/mapred-site.xml
nano $HADOOP_HOME/etc/hadoop/mapred-site.xml
```
Tambahkan:
```bash
<configuration>
 <property>
   <name>mapreduce.framework.name</name>
   <value>yarn</value>
 </property>
</configuration>
```
yarn-site.xml
```bash
nano $HADOOP_HOME/etc/hadoop/yarn-site.xml
```
Tambahkan:
```bash
<configuration>
 <property>
   <name>yarn.nodemanager.aux-services</name>
   <value>mapreduce_shuffle</value>
 </property>
</configuration>
```
Tambahkan Worker Nodes
```bash
nano $HADOOP_HOME/etc/hadoop/workers
```
Isi dengan:
```bash
slave1_hostname
slave2_hostname
```




