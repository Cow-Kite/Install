# 1. Hadoop 다운로드

    mkdir tools
    cd tools
    wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz
    tar -xvf hadoop-3.3.4.tar.gz
    ln -s hadoop-3.3.4 hadoop

# 2. 환경변수 설정

    vim ~/.bashrc

    # 맨 아래로 스크롤
    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64<java version>
    export HADOOP_HOME=/home/<user이름>/tools/hadoop/
    export PATH=$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin/:$HADOOP_HOME/sbin
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HADOOP_HOME/lib/native

# 3. 파일 수정 (/etc/hadoop/)
### 3-1. core-site.xml

    <configuration>
       <property>
            <name>fs.defaultFS</name>
            <value>hdfs://MN:9000</value>
        </property>
    </configuration>

### 3-2. hdfs-site.xml

    <configuration>
        <property>
            <name>dfs.replication</name>
            <value>2</value>
        </property>
        <property>
            <name>dfs.namenode.secondary.http-address</name>
            <value><secondnode 이름>:9868</value>
        </property>
        <property>
            <name>dfs.namenode.name.dir</name>
            <value>file:/home/<user 이름>/tools/hadoop/hadoopdata/hdfs/namenode</value>
        </property>
        <property>
            <name>dfs.datanode.data.dir</name>
            <value>file:/home/<user 이름>/tools/hadoop/hadoopdata/hdfs/datanode</value>
        </property>
    </configuration>

### 3-3. yarn-site.xml

    <configuration>    
        <property>
            <name>yarn.nodemanager.aux-services</name>
            <value>mapreduce_shuffle</value>
        </property>
        <property>
            <name>yarn.nodemanager.env-whitelist</name>
            <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_HOME,PATH,LANG,TZ,HADOOP_MAPRED_HOME</value>
        </property>
        <property>
            <name>yarn.resourcemanager.hostname</name>
            <value>MN</value>
        </property>
    </configuration>

### 3-4. mapred-site.xml

    <configuration>
      <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
      </property>
      <property>
        <name>mapreduce.application.classpath</name>
        <value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
      </property>
    </configuration>


### 3-5. hadoop-env.sh

    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64<java version>

### 3-6. workers (worker node 이름)

    hpc01
    hpc03

# 4. Hadoop 실행 (master node)

    hadoop namenode -format
    
    #sbin/
    start-all.sh
