# Web App on IKS 

How to create a simple Web App on IBM Cloud Kubernetes Service

### 1- Created Cluster 
* Prerequisites 
  - IBM Cloud Acoount 

https://console.bluemix.net/docs/containers/container_index.html#clusters_gs

### 2- Validate is Cluster is Running 

download kubeconfig zip file from ibm cloud (Access Option)
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
### 3- Validate Resource on IKS Cluster 

Vaidate cpu Allocatable in Started Cluster - 1920m

```
$ kubectl get svc --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
...
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource  Requests        Limits
  --------  --------        ------
  cpu       518m (26%)      448m (23%)
  memory    496146Ki (16%)  1323296Ki (45%)
...

```

### 3- Coming Soon 

