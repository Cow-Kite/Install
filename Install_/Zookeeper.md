# 1. Zookeeper 다운로드

    mkdir tools
    cd /tools
    wget https://dlcdn.apache.org/zookeeper/zookeeper-3.8.0/apache-zookeeper-3.8.0-bin.tar.gz
    tar -xvf apache-zookeeper-3.8.0-bin.tar.gz
    ln -s apache-zookeeper-3.8.0-bin zookeeper

# 2. 환경 설정
### 2-1. Data Directory 생성

    mkdir /tools/zoo_data
    vim /tools/zoo_data/myid
    # mn=0, hpc01=1, hpc03=3

### 2-2. zoo.cfg 설정

    cp conf/zoo_sample.cfg conf/zoo.cfg
    vim conf/zoo.cfg

    dataDir=/home/sykang/tools/zoo_data
    clientPort=2181

    server.0=MN:2888:3888
    server.1=HPC01:2888:3888
    server.3=HPC03:2888:3888

### 3. Zookeeper 실행

    bin/zkServer.sh start