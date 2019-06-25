# IBM Cloud Kubernetes Services 

How to deploy a simple NGINX on IBM Cloud Kubernetes Service.

The free cluster has one virtual worker node that is grouped into a worker pool, with 2 CPU, 4 GB memory, and a single 100 GB SAN disk available for your apps to use. 

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

Vaidate cpu allocatable in started cluster - 1920m

```
$ kubectl describe node --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
...
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource  Requests        Limits
  --------  --------        ------
  cpu       518m (26%)      448m (23%)
  memory    496146Ki (16%)  1323296Ki (45%)
...

```

### 3- Deploy NGINX on IKS

Using the nginx_deployment.yaml file 

```
$ kubectl apply -f nginx_deployment.yaml  --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
deployment.apps/nginx-deployment configured
$ kubectl get pod --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
NAME                               READY   STATUS    RESTARTS   AGE
nginx-deployment-d44749686-vkmml   1/1     Running   0          12m
$ kubectl port-forward  nginx-deployment-5cddcdff4d-xw4w5  9999:80  --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
```
Validate Welcome to nginx! Page  http://localhost:9999 

Nota : In this step , NGINX is not reachable from outside cluster. The command $kubectl port-fordward give to capability to access to inside kubernetes cluster.  

### 4- Expose NGINX to Internet 



### Resource 

+ https://cloud.ibm.com/docs/containers?topic=containers-getting-started

