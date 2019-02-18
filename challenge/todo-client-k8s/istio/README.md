### Desplegar recursos relacionados con istio
```
oc apply -f gateway.yaml
```

### Desplegar microservicios
```
oc apply -f <(istioctl kube-inject -f ../todo-client.yaml)
# check proxy has been injected (todo-client,istio-proxy should appear)
oc get deployment todo-client -o wide

oc apply -f <(istioctl kube-inject -f ../../todo-repo-k8s/todo-repo.yaml)
# check proxy has been injected (todo-repo,istio-proxy should appear)
oc get deployment todo-repo -o wide
```

## Para probar determinados casos de uso, es suficiente con aplicar los .yaml correspondientes:
```
kubectl apply -f timeouts.yaml
kubectl delete -f timeouts.yaml
```

## Circuit Breaker

```kubectl apply -f circuit-breaker.yaml```

Una vez aplicada la plantilla, las pruebas a realizar están plasmadas en el fichero `circuit-breaker.md`


## Fault Injection

```kubectl apply -f 404.yaml```
