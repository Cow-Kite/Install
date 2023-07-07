# 1. Ray 설치

    # 기본 기능만 설치
    pip install ray

    # 추가 기능도 설치 (예를 들어, rllib & serve & tune)
    pip install "ray[rllib, serve, tune]" == 2.2.0

### dashboard 포함 설치

    pip install -U "ray[default]"

# 2. Pydantic version 변경

    pip install pydantic==1.10.8

# 3. 환경 변수 설정

    export PATH=$PATH:~/.local/bin

# 4. Ray Cluster 구성

### 4.1 head node

    ray start --head

### 4.2 worker node

    #To add another node to this Ray cluster, run
    ray start --address='192.168.0.200:6379'
    
# 5. Dashboard 외부 접속 허용

    ray start --head --dashboard-host "0.0.0.0"

# 6. Ray Cluster

    ray.init(address='auto')

