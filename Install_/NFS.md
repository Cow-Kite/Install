# 1. 공개키 배포 (마스터에서만 수행)
### 1-1.directory 생성 후 키 생성

    mkdir ~/.ssh
    ssh-keygen -t rsa -P ""

### 1-2. 마스터의 공개 키를 모든 워커에 복사

    ssh-copy-id -i /home/sykang(사용자 아이디)/.ssh/id_rsa.pub MN
    ssh-copy-id -i /home/sykang(사용자 아이디)/.ssh/id_rsa.pub SN01
    ssh-copy-id -i /home/sykang(사용자 아이디)/.ssh/id_rsa.pub SN02 

### 1-3. 모든 노드 ssh 재시작

    service sshd restart

# 2. NFS-Server (마스터에서만 수행)
### 2-1. nfs-kernel-server 설치
    sudo apt-get update
    sudo apt install nfs-kernel-server

### 2-2. 공유 디렉토리(nfs) 생성

    mkdir -p nfs
    chmod -R 777 nfs

### 2-3. NFS 서버 설정 (/etc/exports)

    sudo vim /etc/exports

    # exports
    /home/sykang/nfs *(rw,sync,no_subtree_check)

### 2-4. 설정 마무리

    sudo exportfs -a
    sudo systemctl restart nfs-kernel-server

# 3. NFS-Client (워커에서만 수행)
### 3-1. nfs-common 설치
    sudo apt-get update
    sudo apt install nfs-common

### 3-2.NFS 클라이언트에서 마운트

    mkdir -p nfs
    sudo mount <NFS 서버 IP 또는 호스트 이름>:/home/sykang/nfs home/sykang/nfs
    
