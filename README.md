# Web App on IKS 

How to create a simple Web App on IBM Cloud Kubernetes Service

### 1- Created Cluster 
* Prerequisites 
  - IBM Cloud Acoount 

https://console.bluemix.net/docs/containers/container_index.html#clusters_gs

### 2- Validate is Cluster is Running 

download kubeconfig zip file 
```
$ mkdir imbcloud
$ cd ibmcloud
$ cp /path/kubeconfig . 
$ unzip kubeconfig
$ kubectl --kubeconfig ./kubeConfig286848492/kube-config-hou02-mycluster.yml get nodes
NAME           STATUS   ROLES    AGE   VERSION
10.47.79.213   Ready    <none>   27m   v1.12.7+IKS
$ export KUBECONFIG=$HOME/ibmcloud/kubeConfig286848492/kube-config-hou02-mycluster.yml 
$ kubectl get nodes 
NAME           STATUS   ROLES    AGE   VERSION
10.47.79.213   Ready    <none>   27m   v1.12.7+IKS
```

### 3- Deploy Container on Cluster 


### 4- Expose service to World 


### 5- Local Enviroment to develop Web App ( node , npm , vue-cli )
Vue-js + IKS 

* macOS 
```
$ brew update
$ brew doctor
$ brew upgrade node  # update or install 
$ node -v            # command to validate version of node
v11.11.0 
$ npm install -g npm # update npm
$ npm -v
6.9.0
$ npm install -g @vue/cli 
OR 
$ npm update npm update -g @vue/cli # is installed
$ vue --version
3.5.1

```
Done de Prerequisites


