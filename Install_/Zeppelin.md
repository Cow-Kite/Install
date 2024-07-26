# 1. Zeppelin 다운로드

    wget https://dlcdn.apache.org/zeppelin/zeppelin-0.10.1/zeppelin-0.10.1-bin-all.tgz
    tar -xvf zeppelin-0.10.1-bin-all.tgz
    ln -s zeppelin-0.10.1 zeppelin

# 2. Zeppelin 설정 파일 수정 (Zeppelin/conf/)
### 2-1. Zeppelin-env.sh

    cp zeppelin-env.sh.template zeppelin-env.sh

    export HADOOP_HOME=/home/sykang/tools/hadoop
    export HADOOP_CONF=$HADOOP_HOME/etc/hadoop
    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
    export SPARK_MASTER=yarn
    export SPARK_HOME=/home/sykang/tools/spark
    export ZEPPELIN_ADDR=0.0.0.0
    export ZEPPELIN_PORT=6211 <원하는 포트>

### 2-2. Zeppelin-site.xml

    cp zeppelin-site.xml.template zeppelin-site.xml

    <property>
        <name>zeppelin.server.addr</name>
        <value>0.0.0.0</value>
        <description>Server binding address</description>
    </property>

    <property>
        <name>zeppelin.server.port</name>
        <value>원하는 포트</value>
        <description>Server port.</description>
    </property>

    <property>
        <name>zeppelin.jobmanager.enable</name>
        <value>true</value>
        <description>The Job tab in zeppelin page seems not so useful instead it cost lots of memory and affect the performance.
        Disable it can save lots of memory</description>
    </property>

### 2-3. shiro.ini

    cp shiro.ini.template shiro.ini

    #[users]
    #ID = passwd, role
    sykang = 1234, admin

### 2-4. interpreter.json

    SPARK_HOME: /home/sykang/tools/spark
    spark.master: yarn
    spark.submit.deployMode: cluster
    PYSPARK_PYTHON: python3
    PYSPARK_DRIVER_PYTHON: python3
    spark.executor.instances: 워커 노드 수








