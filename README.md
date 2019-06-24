# Web App on IKS 

How to create a simple Web App on IBM Cloud Kubernetes Service

### 1- Created Cluster 
* Prerequisites 
  - IBM Cloud Acoount 

https://console.bluemix.net/docs/containers/container_index.html#clusters_gs

### 2- Validate is Cluster is Running 

download kubeconfig zip file from ibm cloud ( Access Option)
```
$ mkdir imbcloud
$ cd ibmcloud
$ cp /path/kubeconfig . 
$ unzip kubeconfig
$ kubectl get node --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
NAME           STATUS   ROLES    AGE   VERSION
10.76.68.175   Ready    <none>   18m   v1.13.7+IKS
$ export KUBECONFIG=$HOME/ibmcloud/kubeConfig311401334/kube-config-hou02-mycluster.yml
$ kubectl get nodes 
NAME           STATUS   ROLES    AGE   VERSION
10.76.68.175   Ready    <none>   18m   v1.13.7+IKS
```


