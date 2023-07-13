# Prometheus 다운로드

    wget https://github.com/prometheus/prometheus/releases/download/v2.37.8/prometheus-2.37.8.linux-amd64.tar.gz
    tar xvfz prometheus-2.37.8.linux-amd64.tar.gz
    cd prometheus-*

# Prometheus 실행

    ./prometheus --config.file=/tmp/ray/session_latest/metrics/prometheus/prometheus.yml


# Dashboard 접속

    http://IP주소:9090