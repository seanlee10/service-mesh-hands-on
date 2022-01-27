# service-mesh-hands-on

## Prerequisite
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
- [eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html)
- [istioctl](https://istio.io/latest/docs/setup/getting-started/#download) (Optional)

```bash
# Create EKS Cluster
eksctl create cluster -f eksctl/cluster.yaml

# Create Kubeconfig
aws eks update-kubeconfig --name ###YOUR_CLUSTER### --region ap-northeast-2 --role-arn ###IAM_ROLE###
```

## Istio

> Did you know?
> Istio means "Sail" in Greek

![](./assets/virtualservices-destrules.jpg)


### 1. Install Istio using pre-generated manifest 
```bash
kubectl apply -f istio/01_istio.yaml
```
or
```
istioctl install --set profile=default -y 
```

### 2. Install Kiali
```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/master/samples/addons/kiali.yaml
```

### 3. Install Gateway
```
kubectl apply -f istio/02_gateway.yaml
```

### 4. Install Sample App
```
kubectl apply -f sampleapp
```

### 5. Install VirtualService
```
kubectl apply -f istio/03_virtualservice.yaml
```

### 6. Install DestinationRule
```
kubectl apply -f istio/04_destinationrule.yaml
```

### 7. Test Traffic Routing
```
while sleep 2; do curl ###YOUR_ALB_DNS_NAME###; done
```
