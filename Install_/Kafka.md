# 1. Kafka 다운로드

    mkdir tools
    cd /tools
    wget https://archive.apache.org/dist/kafka/3.2.1/kafka_2.13-3.2.1.tgz 
    tar -xvf kafka_2.13-3.2.1.tgz 
    ln -s kafka_2.13-3.2.1 kafka

# 2. 환경변수 설정

    echo 'export KAFKA_HOME=/home/sykang/tools/kafka' >> ~/.bashrc
    source ~/.bashrc

# 3. Kafka data_dir 생성

    mkdir -p /tools/kafka/logs

# 4. Server.properties 설정

    vim /home/sykang/tools/kafka/config/server.properties
    
    broker.id=(mn=0, hpc01=1, hpc03=3)
    listener=PLAINTEXT://:9092
    advertised.listeners=PLAINTEXT://(MN, HPC01, HPC03):9092
    log.dirs=/home/sykang/tools/kafka/logs
    zookeeper.connect=MN:2181, HPC01:2181, HPC03:2181/kafka-znode

# 5. Zookeeper 실행

    /tools/zookeeper/bin/zkServer.sh start

# 6. Kafka 실행 

    /tools/kafka/bin/kafka-server-start.sh -daemon /home/sykang/tools/config/server.properties
    
