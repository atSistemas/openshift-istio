# Install istio in Minishift
## Steps to install istio

*  **Create a new Minishift profile named servicemesh**
```
$ minishift profile set servicemesh
```
* **Use 8GB of memory for Istio and apps that you might deploy later**
```
$ minishift config set memory 8GB
```
* **4 CPUs results in a maximum of 30 pods, since Istio deploys approximately 9 pods at minimum**
```
$ minishift config set cpus 4
```
* **Caches the downloaded container images for future use**
```
$ minishift config set image-caching true
```
* **Pinning OpenShift version to v3.10.0, so that upgrade of minishift does not recreate the OpenShift cluster**
```
$ minishift config set openshift-version v3.10.0
```
* **Creates a new user called admin with cluster-admin role**
```
$ minishift addon enable admin-user
```
* **Allows containers within OpenShift to be run with any user id**
```
$ minishift addon enable anyuid
```
* **Install istio addon**
```
$ git clone https://github.com/minishift/minishift-addons
$ minishift addon install ./minishift-addons/add-ons/istio
```
* **Deploy istio in Minishift**
```
$ minishift addon enable istio
$ minishift addon apply istio
```
* **Since we have set the profile to be servicemesh, this command starts Minishift with profile servicemesh**
```
$ minishift start --vm-driver=virtualbox
```
## Install cli OpenShift (oc)
* **Download package openshift oc**
```
$ wget https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
```
* **Now, extract the downloaded file. In linux use tar**
```
$ tar –xvf openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
```
* **Change the name file to something small**
```
$ mv openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz oc-tool
$ cd oc-tool
```
* **In this folder, you will find the oc command which will be used for all operarions.Store this path in your .bashrc file**
```
$ export PATH=<HOME>/oc-tool:$PATH
```
## Install cli istio (istioctl)
```
$ curl -L https://git.io/getIstio | sh -
$ export PATH="$PATH:/home/YOUR_USERNAME/istio-kiali/istio-1.0.2/bin"
```
## Note
* With the installation of the istio addon, the add-ons admin-cluster and anyid are applied
* In the binary distribution of istioctl there are examples in the path '/istio-1.0.2/samples/bookinfo/platform/kube/' to be able to deploy several services adding istio functionality - bookinfo.yaml - (not reached to test 100%)
