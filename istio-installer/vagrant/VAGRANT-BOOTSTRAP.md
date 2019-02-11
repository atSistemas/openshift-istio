# OKD 3.11 Bootstrap

Run okd 3.11 locally using vagrant and install istio

## Requirements
- 8 GB RAM
- vagrant
- virtualbox

## Istio installation flavours
- via istio (vagrant-istio)
- via helm (vagrant-istio-helm)

## Bootstrap
``` bash
vagrant up
```

## Access to cluster
``` bash
oc login -u admin -p password https://console.192.168.77.21.nip.io:8443/ --insecure-skip-tls-verify
```