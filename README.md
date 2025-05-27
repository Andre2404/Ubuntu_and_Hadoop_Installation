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

```bash
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```


```bash
source ~/.bashrc
```





