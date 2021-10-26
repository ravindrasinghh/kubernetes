Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.


The name Kubernetes originates from Greek, meaning helmsman or pilot. Google open-sourced the Kubernetes project in 2014. Kubernetes builds upon a decade and a half of experience that Google has with running production workloads at scale, combined with best-of-breed ideas and practices from the community.

Generating Pod Manifests via CLI
1. Create a Pod from Nginx Image



kubectl run [NAME-OF-POD] --image=[IMAGE=NAME] --restart=Never



kubectl run nginx --image=nginx --restart=Never


2. Create a Pod and Expose a Port


kubectl run nginx --image=nginx --port=80 --restart=Never

3. Output the Manifest File


kubectl run nginx --image=nginx --port=80 --restart=Never --dry-run -o yaml


. Create a service - Exposing Pod



kubectl expose pod nginx --name nginx-svc --port=80 --target-port=80



2. Create a service - Expose Deployment



kubectl expose deployment nginx --name nginx-dep-svc --port=80 --target-port=8000



3. Create a NodePort Service



kubectl expose deployment nginx --name nodeport-svc --port=80 --target-port=8000 --type=NodePort




Which namespace has the blue pod in it?
kubectl get pods --all-namespaces | grep blue

Create a service redis-service to expose the redis application within the cluster on port 6379.
kubectl expose pod redis --type=ClusterIP --port=6379 --name=redis-service 


Manually schedule the pod on node01.
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  nodeName: node01
  containers:
  -  image: nginx
     name: nginx



We have deployed a number of PODs. They are labelled with tier, env and bu. How many PODs exist in the dev environment?  
 kubectl get pods --selector env=dev --no-headers | wc -l   

How many objects are in the prod environment including PODs, ReplicaSets and any other objects?
kubectl get all --selector env=prod
Identify the POD which is part of the prod environment, the finance BU and of frontend tier?
kubectl get pods --selector env=prod,bu=finance,tier=frontend


taint and tolerations



apiVersion: apps/v1
kind: Deployment
metadata:
  name: red
spec:
  replicas: 2
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: node-role.kubernetes.io/master
                operator: Exists
