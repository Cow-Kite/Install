# 1. kubernetes-dashboard 설치

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml

# 2. user 생성
### 2-1. Service Account

    apiVersion: v1
    kind: ServiceAccount
    metadata:
    name: admin-user
    namespace: kubernetes-dashboard

### 2-2. ClusterRoleBinding

    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
    name: admin-user
    roleRef:
    apiGroup: rbac.authorization.k8s.io
    kind: ClusterRole
    name: cluster-admin
    subjects:
    - kind: ServiceAccount
    name: admin-user
    namespace: kubernetes-dashboard

### 2-3. Create Token

    kubectl create token admin-user -n kubernetes-dashboard

# 3. dashboard service NodePort로 변경

    kubectl edit service kubernetes-dashboard -n kubernetes-dashboard

    spec:
    clusterIP: 10.111.226.161
    clusterIPs:
    - 10.111.226.161
    internalTrafficPolicy: Cluster
    ipFamilies:
    - IPv4
    ipFamilyPolicy: SingleStack
    ports:
    - port: 443
        protocol: TCP
        targetPort: 8443
    selector:
        k8s-app: kubernetes-dashboard
    sessionAffinity: None
    type: NodePort  # ClusterIP -> NodePort 
    status:
    loadBalancer: {}
