### Desplegar recursos relacionados con istio
```
kubectl apply -f gateway.yaml
```

### Desplegar microservicios
```
kubectl apply -f <(istioctl kube-inject -f service.yaml)
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
