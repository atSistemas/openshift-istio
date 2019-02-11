# OKD 3.11 Bootstrap

Run okd 3.11 locally using vagrant

## Requirements
- 8 GB RAM
- vagrant
- virtualbox

## Bootstrap
``` bash
vagrant up
```

## Access to cluster
``` bash
oc login -u admin -p password https://console.192.168.77.21.nip.io:8443/ --insecure-skip-tls-verify
```