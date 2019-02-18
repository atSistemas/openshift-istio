# Challenge
Esta carpeta contiene los descriptores de despliegue de los microservicios utilizados para el challenge

# Deploy services
``` bash
# manual injection
oc apply -f <(istioctl kube-inject -f apps/todo-client.yaml)
oc apply -f <(istioctl kube-inject -f apps/todo-repo.yaml)
oc apply -f apps/networking.yaml
```

## Escenario 1 - http-errors - 404 aleatorio (50%)
``` bash
# parcheamos el deployment con este escenario
oc patch deployment todo-repo --patch '{"spec": {"template": {"metadata": {"labels": {"version": "http-errors"}}}}}'
# creamos un todo en repo y accedemos por cliente (50% 200/404)
oc apply -f scenarios/http-errors/main.yaml
# clean up
oc patch deployment todo-repo --patch '{"spec": {"template": {"metadata": {"labels": {"version": "all-ok"}}}}}'
oc apply -f apps/networking.yaml
```

## Escenario 2 - delay
``` bash
# parcheamos el deployment con este escenario
oc patch deployment todo-repo --patch '{"spec": {"template": {"metadata": {"labels": {"version": "delay"}}}}}'
# desplegamos el virtual service con delay(repo 7s)
oc apply -f scenarios/delay/main.yaml
# creamos un todo en repo y accedemos por cliente y observamos delay de 7s (inspect, network view)
# clean up
oc patch deployment todo-repo --patch '{"spec": {"template": {"metadata": {"labels": {"version": "all-ok"}}}}}'
oc apply -f apps/networking.yaml
```