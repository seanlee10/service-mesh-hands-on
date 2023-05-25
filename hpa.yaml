# Metric Server 설치 https://docs.aws.amazon.com/eks/latest/userguide/metrics-server.html
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

# HPA 생성 - CPU 50%를 기준으로 새롭게 Pod을 생성
kubectl autoscale deployment frontend --cpu-percent=50 --min=1 --max=10

# 부하발생
kubectl run load-generator \
 --image=williamyeh/hey:latest \
 --restart=Never -- -c 10 -q 5 -z 60m http://frontend.default.svc.cluster.local

# HPA 기록 모니터링
kubectl get hpa frontend -n default --watch
