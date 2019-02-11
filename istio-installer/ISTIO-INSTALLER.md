### INSTALACIÓN
Según la documentación de Istio, es recomendable utilizar Helm para la instalación de Istio:

Descargar release de Helm y descomprimir para iniciarlo en el cluster

##Iniciar Helm
```
./helm init --service-account tiller
```

##Istio
```
curl -L https://git.io/getLatestIstio | sh -
cd istio-1.0.5
export PATH=$PWD/bin:$PATH
```

##Para desplegar aplicaciones es necesario otorgar permisos a las serviceaccounts que crearemos:
```
oc adm policy add-scc-to-user anyuid -z istio-ingress-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z default -n istio-system
oc adm policy add-scc-to-user anyuid -z prometheus -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-egressgateway-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-citadel-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-ingressgateway-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-cleanup-old-ca-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-mixer-post-install-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-mixer-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-pilot-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-sidecar-injector-service-account -n istio-system
oc adm policy add-scc-to-user anyuid -z istio-galley-service-account -n istio-system
```

Al utilizar Helm se le pueden tanto parametrizar por ejemplo, el tipo de servicio:
```
helm install install/kubernetes/helm/istio --name istio --namespace istio-system --set gateways.istio-ingressgateway.type=NodePort --set gateways.istio-egressgateway.type=NodePort
```

##To upgrade Istio:
```
helm upgrade istio install/kubernetes/helm/istio --namespace istio-system --set gateways.istio-ingressgateway.type=NodePort --set gateways.istio-egressgateway.type=NodePort --set kiali.enabled=true
```

## Para darle permisos a Kiali en Openshift (privileged o view):
```
oc policy add-role-to-user privileged system:service:account:istio-system:kiali-service-account -n management-infra
oc policy add-role-to-user view system:serviceaccount:istio-system:kiali-service-account -n management-infra
```

### EJEMPLOS DE DESPLIEGUE (Mirar documentación oficial, todos estos ejemplos vienen en el repositorio de istio)

Para probar el despliegue que viene junto con la documentación:
```
oc apply -f <(istioctl kube-inject -f samples/bookinfo/platform/kube/bookinfo.yaml)
```

##Desplegar gateway
```
oc apply -f samples/bookinfo/networking/bookinfo-gateway.yaml
```

# oc get gateway
NAME               AGE
bookinfo-gateway   17s


Set the ingress host:
```
export INGRESS_HOST=$(oc get po -l istio=ingressgateway -n istio-system -o 'jsonpath={.items[0].status.hostIP}')
```
Set the ingress ports:
```
export INGRESS_PORT=$(oc -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')
export SECURE_INGRESS_PORT=$(oc -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].nodePort}')
```

Set the GATEWAY_URL:
```
export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT
```
Test if app is working:
```
curl -o /dev/null -s -w "%{http_code}\n" http://${GATEWAY_URL}/productpage
# Response: 200
```


## INTELLIGENT ROUTING

# Request Routing

Para aplicar reglas para la aplicación de ejemplo:
```
oc apply -f samples/bookinfo/networking/destination-rule-all.yaml
```

Para empezar a crear reglas de enrutamiento:
```
oc apply -f samples/bookinfo/networking/virtual-service-all-v1.yam
```

Para enrutar según el usuario
```
oc apply -f samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml
```

Para limpiar el entorno de virtual services:
```
oc delete -f samples/bookinfo/networking/virtual-service-all-v1.yaml
```


Traffic shifting (Migrar tráfico gradualmente)
```
oc apply -f samples/bookinfo/networking/virtual-service-reviews-50-v3.yaml
```

Una vez la versión v3 esté estable, se dirige todo el tráfico a esta versión:
```
oc apply -f samples/bookinfo/networking/virtual-service-reviews-v3.yaml
```

### I'M WORKING ON IT

Para habilitar el auto-injection es necesario habilitarlo por namespaces:
```
oc label namespace default istio-injection=enabled
```

En el directorio `helm` hay un Chart para probar despliegues adaptado a Istio (still not working)
