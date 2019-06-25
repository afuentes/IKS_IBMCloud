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

### 4- Expose NGINX to World 

```
$ kubectl apply -f nginx_service.yaml  --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
$ kubectl describe service nginx-service  --kubeconfig=./kubeConfig311401334/kube-config-hou02-mycluster.yml
Name:                     nginx-service
Namespace:                default
Labels:                   <none>
Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                            {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{"service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features":"i...
                          service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: ipvs
Selector:                 app=nginx-deployment
Type:                     NodePort
IP:                       172.21.19.42
Port:                     http  80/TCP
TargetPort:               80/TCP
NodePort:                 http  30275/TCP
Endpoints:                172.30.60.74:80
Session Affinity:         None
External Traffic Policy:  Local
Events:                   <none>
```

### 5- Access to IKS from Internet using NodePort & Public IP  

1- Public IP from Console 
Validate the Public IP from IBM Cloud Console (IBM Cloud --> Clusters --> mycluster --> Worker Nodes --> Public IP)

2- Public IP using ibmcloud command 

```
$ ibmcloud cs workers mycluster
OK
ID                                                 Public IP        Private IP     Machine Type   State    Status   Zone    Version   
kube-hou02-pa792b4d0fad7b484688b3da914f059689-w1   173.193.99.137   10.76.68.175   free           normal   Ready    hou02   1.13.7_1527  
```

the url is http://<public ip>:<NodePort>

```
$ curl http://173.193.99.137:31747 
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
DONE !!!

### Resource 

+ https://cloud.ibm.com/docs/containers?topic=containers-getting-started
+ https://www.ibm.com/cloud/blog/announcements/kubernetes-v1-13-2-is-now-available-in-ibm-cloud-kubernetes-service

