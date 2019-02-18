# OKD 3.11 Bootstrap

Run okd 3.11 on steroids with istio locally using vagrant

## Requirements
- 8 GB RAM
- vagrant
- virtualbox

## Bootstrap
``` bash
vagrant up
```

## Deploy Istio
``` bash
$ vagrant ssh

## dentro de la vm
./vagrant/istio-bootstrap
```

## Access to cluster
``` bash
oc login -u admin -p password https://console.192.168.77.21.nip.io:8443/ --insecure-skip-tls-verify
```