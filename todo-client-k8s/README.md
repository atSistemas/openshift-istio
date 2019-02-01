### Desplegar recursos relacionados con istio
kubectl apply -f gateway.yaml

### Desplegar microservicios

kubectl apply -f <(istioctl kube-inject -f service.yaml)
