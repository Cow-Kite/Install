# 1. Spark 다운로드
    
    cd tools/
    wget https://archive.apache.org/dist/spark/spark-3.2.3/spark-3.2.3-bin-hadoop3.2.tgz
    tar –xvf spark-3.2.3-bin-hadoop3.2.tgz
    ln -s spark-3.2.3-bin-hadoop3.2 spark

# 2. 환경변수 설정 

    echo "export SPARK_HOME=/home/sykang/tools/spark/" >> ~/.bashrc
    source ~/.bashrc

# 3. data_dir 생성

    mkdir -p /spark/eventLog

# 4. 환경 설정
### 4-1. conf/spark-defaults.conf

    cp spark-defaults.conf.template spark-defaults.conf

    vim spark-defaults.conf
    spark.master	                        yarn
    spark.eventLog.enabled 	                true
    spark.eventLog.dir	                    file:///home/sykang/tools/spark/eventLog
    spark.history.fs.logDirectory           file:///home/sykang/tools/spark/eventLog

### 4-2. conf/workers

    cp workers.template workers

    vim workers
    hpc01
    hpc03

### 4-3. conf/spark-env.sh

    cp spark-env.sh.template spark-env.sh

    vim spark-env.sh
    export SPARK_SSH_OPTS="-p 10022" 
    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 
    export SPARK_MASTER_HOST=MN 
    export HADOOP_HOME=/home/sykang/tools/hadoop 
    export YARN_CONF_DIR=/home/sykang/tools/hadoop/etc/hadoop 
    export HADOOP_CONF_DIR=/home/sykang/tools/hadoop/etc/hadoop

# 5. 실행
### 5-1. Hadoop 실행 (master)

    /tools/hadoop/sbin/start-all.sh

### 5-2. Spark 실행 (master)

    /tools/spark/sbin/start-all.sh





