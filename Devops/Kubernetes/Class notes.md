## 05/09/23
## Kubernetes

- Kubernetes (k8s) is an open source orchestrator for deploying containerized applications.

- K8s provides the following features:-
  - Development Velocity
  - Scaling
  - Abstract your infrastructure
  - Self Healing
  - Declarative Approach

## 07/09/23

### K8s-Installaton

[Kubernetes + CRI + DOCKER]

- Kunernetes has dose not suport to Docker directly
  we need to install CRI (Container Runtime Interface) Component...

- Install those commands in `Master node` and `worker node`
  1. kubeadm (A tool used to build k8s clusters)
  - install container runtime (CRI)
[Docker Engine does not implement CRI which is a requirement for a container runtime to work with Kubernetes]
[https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/]
  - Required ports
[https://kubernetes.io/docs/reference/networking/ports-and-protocols/]

  2. kubectl
  - Kubernetes-specific command line tool that lets you communicate and control Kubernetes clusters.

  3. kubelet
  - The primary "node agent" that runs on each node.
---xx---

# Installation steps

    - Each matchine have atleast 2vcpus and 4GB RAM

 1. Controle plane (master-node)       --------RT (18:20)
    install those softwares
  [docker, cri-dockerd, kubeadm, kubectl, kubelet]

# Docker
```sh
install docker (docer script install)
sudo usermod -aG docker ubuntu
exit & relogin
```


# Install CRI-dockerd
[https://github.com/Mirantis/cri-dockerd]
  - goto :Using cri-dockerd --> instal --> releases page. 
      Assets --> [https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.4/cri-dockerd_0.3.4.3-0.ubuntu-jammy_amd64.deb]
  copy this link address
```sh
wget https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.4/cri-dockerd_0.3.4.3-0.ubuntu-jammy_amd64.deb

sudo dpkg -i cri-dockerd_0.3.4.3-0.ubuntu-jammy_amd64.deb
```
    - dpkg (Debian Package Manager)- install, remove, and manage individual software packages.


# Installing kubeadm
[https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/]

- Kubernetes package repositories
```sh
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl

curl -fsSL <https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key>
sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] <https://pkgs.k8s.io/core:/stable:/v1.28/deb/> /'
sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

kubectl version
kubeadm version
```
`move to root user`
    ^ sudo -i
now installize the cluster (CRI) - [NOTE:-]no need to give cloud (aws)

# kubeadm init
```sh
kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/cri-dockerd.sock"
```

* connact with 2 nodes
    now copy the commands after kubernetes instialized controle-plane
      mkdir -p $......
      sudo cjp -i.....
      sudo chown $....
      .... 
      ....
      ....
-------xxxxxx-------

`move to normal user` and apply those commands of [kubernetes instialized controle-plane]     ------RT(43:00)
    ^ mkdir -p $......
    ^ sudo cjp -i.....
    ^ sudo chown $....
check the nodes
    ^ kubectl get nodes
    [STATUS : NotReady -- Pod Network is not ready]
---xx---
---xx---

## 2. Node-1

    install those softwares
  [docker,cri-dockerd,kubeadm,kubectl,kubelet]
  * Docker
```sh
install docker (docer script install)
sudo usermod -aG docker ubuntu
exit & relogin
```
- same as master node:-
  - install CRI-dockerd:-
```sh
wget <https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.4/cri-dockerd_0.3.4.3-0.ubuntu-jammy_amd64.deb>

sudo dpkg -i cri-dockerd_0.3.4.3-0.ubuntu-jammy_amd64.deb
```

# Installing kubeadm
```sh
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key
sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
   
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /'
sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
`move to root user` -----RT (45:45)
    ^ sudo -i
-- now execute the join command
    ^ kubeadm jain 172............
    ^ --descovery-tokern-ca........
    ^ --cri-socket "unix:///var/run/cri-dockerd.sock"
--xx--

- Controle plane (master node)
`faninal uploade`
```sh
kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml 
```

    ^ kubectl get nods
ip-172-31-12-245   Ready    <none>          72s   v1.28.2
ip-172-31-8-168    Ready    control-plane   22m   v1.28.2

    ^ kubectl get nodes -o wide
ip-172-31-12-245   Ready    <none>          6m6s   v1.28.2   172.31.12.....
ip-172-31-8-168    Ready    control-plane   27m    v1.28.2   172.31.8......

---xx---
---xx---

- How to POD's communication each other
  - CNI Plugin
  - Kubernetes will not give CNI plugin you need to install it
[https://kubernetes.io/docs/concepts/cluster-administration/addons/]

  - Flannel:-
    - a plugin to support multiple network interfaces in a Kubernetes pod.
    - we used to less IP address
    - it is usease overlay and underlay

===========================================================

## 08/09/23
[https://directdevops.blog/2023/09/08/devops-classroomnotes-08-sep-2023/]

### POD

    * Atomic Unit:
    - a pod is a basic unit of deployment in Kubernetes
    - A pod is the smallest and simplest unit in the Kubernetes object model.
    - It can contain one or more containers, but those containers are always scheduled to run on the same node and share the same network namespace and storage.

- Pod have run the container
  - one contaienr is best for a pod

- Pod have more than one containers
    1. Maincar container
        - its a primary container
        - only one maincar container inthe ever pod
    2. Sidecat container
        - support jobs for maincar
            - set an alert like iam alive
            - try to export logs
        - `n` number of contiaers in pod (depends on application)

- Resource in facebook
  - create an user, group, sending some post, like.....
  - create a resource, update a resource, get the resource, delete the resource ......

# API Server resource in K8s    ------RT (15:00)

    - Ex:- Aadhar card ......
    login kubeadm installation  
         1. master node
         2. node 1

    ^ kubectl get nodes (check the nodes are up)
ip-172-31-12-245   Ready    <none>          21h   v1.28.2
ip-172-31-8-168    Ready    control-plane   21h   v1.28.2

    ^ kubectl api-resources (all supported resources)
    [NAME     SHORTNAMES     APIVERSION       NAMESPACED      KIND]

- NAME:-
  - In this NAME refers to resource that can be manipulated by api-server.
  - Each resource has name and short name
Eg:- NAME= pods,  SHORTNAME= po
         = namespaces,     = ns
         = nods,           = no

- | grep:-
  - a way for searching on the information
    ^ kubectl api-resources | grep pod
        [the way of searching the information about pod]

    ^ kubectl api-resources | grep service
        [information about services]
    ^ kubectl get services
        [same way to find the services]

- what is imperative and declarative

# Imperative:-

    -  It's means constructing a command by command line
    - Imperative configuration involves creating Kubernetes resources directly at the command line against a Kubernetes cluster.
    - this is good for one time creation
Eg:-
  Create a nginx-pod  
    ^ kubectl run nginx --image nginx  [pod/nginx created]
    ^ kebectl get po [nginx is running]

# Declarative:-

    - create a file (yaml) that describes the configuration for resource, and then apply the content of the file to the Kubernetes cluster.
Eg:-
    create a pod
  ^ kubectl apply -f <filename.yaml>
    delete a pod
  ^ kubectl delete -f <filename.yaml>

## Creating Pod Manifests   ------RT (27:30)

- How to i write the file....?
  - kubernetes use to `go` language
[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.28/]

```yaml
---
1. apiVersion: 
2. kind:
3. metadata:
4. spec:
5. [status:]
```

1. # apiVersion:-

    - Which version of the K8s API you're using to create this object.
    - it'll never change something done in the past
    - it's act like bridge
    Eg:- FB give new version and update to the older version, than FB has never give the older version
----xx----

# API Versioning: [K8s API verion-1.28]

     - API Group Refer Here
     - version
[https://kubernetes.io/docs/reference/using-api/]

- if the apiGroup is `core`
    ^ apiVersion: <version>
Eg:-
    ^ kubectl api-resources
  NAME= pods  SHORTNAME= po   APIVERSION= v1
    [here the version is not core]

- if the apiGroup is `not core`
    ^ apiVersion: <apiGroup>/<version>
Eg:-
    ^ kubectl api-resources
  NAME= deployments  SHORTNAME= deploy    APIVERSION= app/v1
    [here the version is not core]

# Alpha:-

    - The version names contain alpha (for example, v1alpha1).
    - K8s recomand to use 
    - it's not to use in production

# Beta:-

    - The version names contain beta (for example, v2beta3).
    - the feture is dised into K8s will adding next changes

# Stable:-

    - The version name is vX where X is an integer.
    - mainly we use 
        eg:- vi 

- How to find the present version of Kubernetes
  - one page reference
[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.28/]

    ^ kubectl version
    clint version: v1.28.1
    Kustomize Version: v5.0.4-0......
    Sercer Version: v1.28.1   [its manage apiVersion]

{if you want to change the version of v1.28
    you can remove the v1.28 to v1.26 like.....}
----xx----
2. # kind:-
    - What kind of object you want to create.

3. # metadata:-

    - Data that helps uniquely identify the object,
                      including a name string,
                      UID (unique identifier),
                      optional namespace.
    - name, labelling, resources .......

4. # spec (specifies):-

    - What state you desire for the object

5. # status:-

    - K8s has automatically add the information about pod
    - no need to add this status.......

- Create a manifest file for nginx pod

--------------------------------------

```yaml
apiVersion: v1
kind: pod
metadata:
  name: hello-pod
spec: 
  containers:
    - name: webserver
      image: nginx:1.25
```

goto mastaer node   -----RT (53:00)
    ^ mkdir manifests --> cd manifests
    ^ vi hello-pod.yaml
paste the content heare

    ^ kubectl apply -f hello-pod.yaml [created a pod]
    ^ kubectl get pods  [list of pods]
    ^ kubectl get pods -o wide [more information of pods]

all information about your pod
    ^ kubectl get pods <name of pod> -o yaml

========================================================================

## 09/09/23

### Pod
[https://directdevops.blog/2023/09/10/devops-classroomnotes-10-sep-2023/]

# Scaling:-

- Increasseing number of pods.
- process of adjusting the number of pods of a particular workload or application.
- two types of scaling

1. # horizontal scaling (Scaling Out)

    - Adding or removing multiple pods of a workload to distribute the load evenly and improve availability.

- ReplicaSets:
        -  Resource of K8s
        - A specified number of pod-replicas are running at all times. You can scale a ReplicaSet up or down to adjust the number of replicas.

- Deployment:
        - Build on ReplicaSets and provide additional features like rolling updates and rollbacks.

- Horizontal Pod Autoscaler (HPA):
        - Automatically adjusts the number of replicas based on resource utilization metrics (CPU and memory) or custom metrics.

2. # vertical scaling (Scaling Up or Down)

    - Adjusting the resources (CPU and memory) allocated to individual pods.

# Autoscaling:-

    - Automatically adjust the number of pods (replicas) in a deployment, replica set, or other workload to meet changing demands or resource utilization targets.

- two main types of autoscaling:-

1. # Horizontal Pod Autoscaling (HPA):-

    - automatically adjusts the number of replicas of a deployment or replica set based on observed CPU or memory utilization or custom metrics.

2. # Cluster Autoscaler:-

    - Automatically adjusts the size of a cluster by adding or removing nodes (VMs) based on resource demand.

3. # Vertical Pod Autoscaler (VPA)

    - adjusting the number of replicas and nodes, Vertical Pod Autoscaler (VPA) focuses on adjusting the CPU and memory resource requests and limits for individual pods.

### How K8s identifies objects: `Labels`

[https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/]

# Labels:-

- Label is a key pair examples are
        app: nginx
        version: v1.0

- Labels are used to seletc/query kubernetes objects.
- Labels are key/value pairs that are attached to objects such as Pods

  - delete pods
        ^ kubectl delete po <pod name>

# Create a POD

--------------

- write a labels in pod
    push the git repository..

```yaml
git clone....
```

    ^ kubectl apply -f nginx-pod-labels.yaml
pod/nginx-pod-labels1 created
pod/nginx-pod-labels2 created
pod/nginx-pod-labels3 created

    ^ kunectl get pods
nginx-pod-labels1   1/1     Running   0             15s
nginx-pod-labels2   1/1     Running   0             15s
nginx-pod-labels3   1/1     Running   0             15s

    ^ kubectl get pods --show-labels
nginx-pod-labels1   1/1   3m52s   app=nginx,env=dev,release=v1.1
nginx-pod-labels2   1/1   3m52s   app=nginx,env=qa,release=v1.1
nginx-pod-labels3   1/1   3m52s   app=nginx,env=uat,release=v1.1
---xx---

# Selecter

    - Selectors in k8s help in querying objects using labels
    - selectors are of two types

1. Equality Based Selectors
    - there are equal are not equal
    ^ kubectl get pods -l env=dev
    ^ kubectl get pods -l env!=dev

2. Set based selectors
    - env=dev or qa ...?
    - version=v1.1 or v1.2 ...?

- ReplicaSet vs ReplicaControlar
  ReplicaSet:-
  - Both (equality and set)
  - Equality based and Set based label selection

  ReplicaControlar:-
  - only equality based label selection

## Pod with container with additional commands  -----RT (32:00)

create new file - cmd-demo.yaml
    add the one more container in the spec:
        - name: logforwarder

```
.........
```

- delete older pod
    ^ kubectl delete -f <nginx-pod-labels.yaml>

- delete all in a file
    ^ kubectl delete -f .

- now run the application
    ^ git pull
    ^ kubectl apply -f <cmd-demo.yaml>
    ^ kubectl get po

get the more information about your pod
    ^ kubectl describe pod <name of the pod>

### Interacting with contianers ----RT (40:00)

    ^ docker container exec -it </bin/bash>or</bin/sh>
   `OR`
    ^ docker container exec

- interacting with tty (terminal)
    if you are running the nginx pod
        goto inside the nginx pod
    ^ kubectl exec <pod name> -it -c -- /bin/bash
now exeute the command
    -> kubectl exec nginx-pod -it -c -- /bin/bash

    ^ kubectl exec <pod name> -it -c <container name> -- /bin/bash
now exeute the command
    -> kubectl exec nginx-pod -it -c logforwarder -- /bin/bash
    ^ ifconfig

## What happens when container goes into exited state   ---RT (48:30)

- Create one file <patientcontainer.yaml>

```
add the content
```

- delete all pods
    ^ kubectl delete -f .

- create new pods
  ^ kubectl get po -w
dedone   0/1     Completed   2 (28s ago)   33s
dedone   0/1     CrashLoopBackOff   2 (12s ago)   35s
dedone   0/1     Completed          3 (30s ago)   53s

:- here the pod status was pending, recreated and complete....
    * Pending state:-
        - API server has accept your reqused and stored in etcd cluster and than....
        - schudular has picup your stuff and recreate a new node (container)...
        - once the container create its gose to completed state
  now the kubernetes try to reaste the container ....

    * CrashLoopBackOff:-
        - in container exet stage at all the time in see kubernetes the error called ad crashloopbackoff...

now describe the pod
    ^ kubectl describe pod <pod name>

---xxxx---

# Resteart polacy....?

## Container types in Pod:-

- init containers:
  - These containers are created prior to actual/main containers. ideally these containers should be short lived and majorly for meeting preconditions to run your application.

- Containers:
  - This is where we run actual applications and they are expected to be living forever (continously)

## Pod Lifecycle:-      ----RT (01:31:00)

[https://directdevops.blog/2019/10/07/docker-logging-docker-memory-cpu-restrictions/]

# Exervise

    - Create a nginx container with 128MB of RAM
    - Create a jenkins container with "0.5" CPU and 256MB of RAM
  Ans:
    ^ docker container run  -P -d  --memory 128m nginx
    ^ docker container run --name r-memcpu-jenkins -P -d --cpus="0.5" --memory 256m jenkins/jenkins
    ^ docker stats

## Resource Restrictions in Pods:-     ----RT (01:52:30)

[https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/]
    - Limits in Resoruce Restrictions mean maximum size that will be allocated (upper bounds/limits) and request are lower limits.

# Exercise

    -  Write the manifest to run above mentioned docker containers in Pod

====================================================================

## 10/09/23 [Mrng]

------------------
[https://directdevops.blog/2023/09/10/devops-classroomnotes-10-sep-2023-2/]

### Controllers

----------------
    - Pod tries to keep containers running, but for us we need to keep Pods running according to some state.
    - Lets understand first two categories

1. Replicas:

- Here we have two resources
    A. ReplicationController (RC)
  - An older version of this controller, now largely replaced by ReplicaSets.
  - write only equality based labels stlecters.

    B. ReplicaSet (RS)
`maintaing the desired state of number of replicase of pod`.
  - specified number of replicas (Pods) of a particular application are running at all times.
  - If Pods fail or additional replicas are needed, the ReplicaSet will create or delete Pods to maintain the desired count.
  - write set based labels also.

- Here our desired state (spec) will be
        - number of replicas
        - pod spec
        - label selector
- These objects try to maintain the desired state of resources within the cluster.

2. Jobs:
    - These will run the Pods which have finite execution time period
Here we have two resources
    A. Job
    B. CronJob

## Create ReplicaSet:-

[https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/]
    - create one new folder `Replicas --> ReplicaSet --> jenkins-rs.yaml

- matchLabels

```yaml
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: jenkins-rs
  labels:
    purpose: rsdemo
spec:
  minReadySeconds: 2
  replicas: 3
  selector:
    # matchLabels:     
      app: jenkins       ----> equlity based lable seletctor  
      release: v1.1       matchexpressions-> set based selector
  template:
    metadata:
      labels:
        app: jenkins
        release: v1.1
    spec:
      containers:
        - name: jenkins
          image: jenkins/jenkins
          ports:
            - containerPort: 8080
              protocol: TCP
```

    ^ kubectl api-resources | grep replica
replicationcontrokkers (RC)
replicasets (RS)
    ^ kubectl apply -f jenkins-rs.yaml
replicaset.apps/jenkins-rs created

    ^ kubectl get rs
jenkins-rs-77c8v   1/1     Running   0          27s
jenkins-rs-plbgw   1/1     Running   0          27s
jenkins-rs-wxc2n   1/1     Running   0          27s

    ^ kubectl get po -o wide
jenkins-rs-77c8v   10.244.1.9    ip-172-31-10-207   <none>           <none>
jenkins-rs-plbgw   10.244.1.10   ip-172-31-10-207   <none>           <none>
jenkins-rs-wxc2n   10.244.1.8    ip-172-31-10-207   <none>           <none>

===xx===

- added matchExxpressions

```yaml
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: jenkins-rs
  labels:
    purpose: rsdemo
spec:
  minReadySeconds: 2
  replicas: 3
  selector:
    matchLabels:
      app: jenkins
      release: v1.1
    # matchExpressions:
    #   - key: app
    #     operator: In
    #     values:
    #       - jenkins
    #       - hudson
    #   - key: release
    #     operator: Exists
  template:
    metadata:
      labels:
        app: jenkins
        release: v1.1
    spec:
      containers: 
        - name: jenkins
          image: jenkins/jenkins
          ports:
            - containerPort: 8080
              protocol: TCP
```

    ^ kubectl apply -f jenkins-rs.yaml
    ^ kubectl get rs
    ^ kubectl get rs
    ^ kubectl get rs -o wide 
    ^ kubectl get rs jenkins-rs

---xx---

- create a pod

    ^ kubectl run ngnix1 --image nginx

# Exercise

    - Write a Replication controller for creating 3 httpd pods

### Jobs and Cron Jobs      ----RT (59:00)

----------------------
NOTE:- Job execute only once and stop but
       CronJob execute multiplule time

# Cron Jobs:-

- Write a Job which runs alpine pod with some script
  - Create new file `jobs` --> `cronjobdemo.yaml`

```yaml
---
apiVersion: batch/v1
kind: CronJob
metadata:
  name: cronjobdemo
  labels:
    purpose: cronjobdemo
spec:
  schedule: '*/5 * * * *'
  jobTemplate:
    metadata:
      labels:
        purpose: jobdemo
    spec:
      backoffLimit: 3
      template:
        metadata:
          labels:
            app: batch
        spec:
          containers:
            - name: batchdemo
              image: alpine
              command:
                - sleep
                - 10s
```

- move to git
Master Node
    ^ git pull
    ^ kubectl apply -f cronjobdemo.yaml
    ^ kubectl get cronjobs.batch
    ^ kubectl get describe cronjobs.batch cronjobdemo

Node-1
    ^ kubectl get jobs -w

Node-2
    ^ kubectl get po -w
===xx===

## Namespace:-      ----RT (02:02:00)

- In K8s namespace is a `logical space` or `logical cluster` in which resources will be created.
-  
    ^ kubectl get po --all-namespaces

## Service in K8s   ----RT (02:04:45)

- Every Pod when created gives a unique ip address and Name
  - When Pods are scaled
- Create a `replicaset with 3 nginx pods` with `label app:nginx`

```yaml
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-rs
  labels:
    app: nginx
    purpose: svcdemo
spec:
  replicas: 3
  minReadySeconds: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginxc
          image: nginx:1.25
          ports:
            - containerPort: 80
              protocol: TCP
```

- Create service (svs)

```yaml
apiVersion: vi
kind: Service
metadata:
  name: nginx-service
  labels:
    app: nginx
spec:
  type: ClusterIP
  selector: 
    app: nginx
  ports:
    - targetPort: 80
      port: 80
```

    ^ git pull
    ^ kubectl apply -f nginx-rs.yaml
    ^ kubectl get po -o wide  

- In side the pod
    ^ kubectl exec c1 -it -- /bin/sh
    ^ ping -c 4 <pod IP>

---xx---

- Cluster API
- Servives (K8s)
- Kube Proxy
  - who will access the services to match the pod and attach
  - responsible for network proxying and load balancing
- Load Balancer
- Network proxying
===================================================================

## 10/09/23 [Even]

------------------

### Servives

[https://directdevops.blog/2023/09/10/devops-classroomnotes-10-sep-2023-3/]

- Create service and 3 nginx pods (yesterday done)
    ^ kubectl apply -f nginx-rs.yaml
    ^ kubectl get po -o wide
here 3 pods are available now
created 3 nginx pods
    ^ kubectl get pods -l app=nginx

create service
    ^ kubectl apply -f nginx-svc.yaml
    ^ kubectl get endpoints nginx-svc
here only show the nginx-svc pod

----

- Describe the all the services
    ^ kubectl describe service nginx-svc

- status of IP
    ^ kubectl get pods -o custom-columns=IP:status.podIP

# outside the cluster (from the node)

- node also part of cluster
    ^ curl <IP>   --> [curl 10.96.75.166]

  if the ports are open add this rules also in maniually in AWS sequrity groups
- add/enabel all sequrity groups (inbond rules)
        all tcp   any ware
        all udp   any ware
        all icmp  any ware

# inside the cluster

    ^ kubectl exec -it <name of the pod> -- /bin/bash
    ^ curl <ip>   ---> curl 10.96.75.166
    ^ curl <pod name>  ---> curl ngix-svc
:- here both IP and NAME are work .....

- Create one example file alpine image `experiment-pod.yaml`

```yaml
---
apiVersion: v1
kind: Pod
metadata: expermental
spec:
  containers:
    - name: expermental
      image: alpine
      command:
        - sleep: 1d
```

    ^ git add .
    ^ git commit -m "added expermetal"
    ^ git push

    ^ git pull
    
    ^ kubectl apply -f experiment-pod.yaml
    ^ kubectl exec -it experimental -- /bin/sh
inside the container
    ^ nslookup nginx-svc
    ^ cat /etc/resolv.conf
default svc cluster
    ^ exit

## Node Port        ---->RT (29:20)

    - A type of service that allows external traffic to reach a service running within a Kubernetes cluster.

- Create a NodePort services
  - Service (svc) ---> nginx-svc-np.yaml
    [there are no differce in service(svc) and node port]

```yaml
---
apiVersion: v1
kind: Service
metadata: 
  name: nginx-svc-np
  label:
    app: nginx
    purpose: svc-np-demo
spce:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 32024
```

    ^ git add commit push
    ^ git pull

    ^ kubectl appy -f nginx-svc-np.yaml
    ^ kubectl get po
now goto instance all nodes public IP copy and find `http://<ip>:32024`
---> NGINX PAGE WILL BE OPEND <----

## Other Service Types:-

    - LoadBalancer
    - External

### Controllers to control rollouts

## Exercises:-

    * Create a nopcommerce pod with the following
        environmental variables:
        purpose = learning

    * Create a namespace called as dev and create the nop commerce pod in dev namespace.

    * Create a nginx rs with service in default namespace and create a nginx res with service in dev namespace.

    * Create a pod called as c1 with alpine in it (default), try accessing the service in default namespace as well as dev namespace.

---xx---
In production we write a

# DeploymentSets

    - Temple ==> ReplicaSet template

# DeamanSet

# StatefullSet

we dont need to write

- podsept
- replicaset
---xx---
===========================================

## Components of ControlePlane (MaserNode) and Node (WorkerNode)

- ControlePlane (MaserNode)  
  - Manages clusters and resources such as Pods and Node.
    - ApiServer
    - Etcd
    - Kubectl
    - Scheduler
    - Controller

- Node
- Kubelet
- Container Run Time
- KubeProxy

- Api Server (Application Programming Interface):-
  - All communications for Kubernetes (External and internal)

- Etcd:-
  - Storge component in K8s
  - distubuted key-value store

- Kubectl (command line tool):-
  - kubectl speacks api server

- Scheduler:-
  - Create a new
  - controle plane process which assigns pods to nodes

- Controler:-
  - Responce for maintaing state

- Cloud controler manager
  - AKE, EKS, GKS

kubernetes works lodes

=============================================================================

## 16/09/23

-----------

### Managed Kubernetes or Kubernetes as a Service

- It is a Cloud Providers.
- Controle-Plane --> managed by Cloud Service Providers (charged hourly)
- Worker-Node --> storage (as usal charges)

- Popular K8s services:
  - AKS (Azure Kubernetes Services)
  - EKS (Elastic Kunernetes Services)
  - GKE (Google Kubernetes Engine)
  - .....
  -
<!-- # AKS (Azure Kubernetes Services)
* Install `kubectl` in your system
```sh
choco install kubernetes-cli
```
  install k8s on azure (kubectl) -->

# DNS Server

- Type record
  - A Record: `domain name to IP` (IPv4)
  - AAAA Record: `domain name to IP` (IPv6)

- C-NAME (Canonical Name)
  - `alias to domain name`

# Service with external name

    - we need not any ports
    - its a name to name maping

```yml
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc-external
  labels:
    app: nginx
    purpose: svcdemo
spec:
  type: ExternalName
  externalName: nginx.qt.com
  selector:
    app: nginx
```

## Deployments:     ------->RT (01:30:00)

[Deployment ---> Replicaset ---> Pod ---> Containers]

- Deployment is a workload which creates
  - Replica Sets: These create
    - Pods: Which inturn creates
      - Containers: This is where the applcation runs.

- Deploymet create a history

- Recreate:
  - Downtime approch, bring down alder versions and recreate new versions.

- Rolling Update : Default
  - RollBack (Undo Rollout):
  - RollOut

- Create a deploy --> nopcommerce-deploy.yaml     ------>RT (01:43:00)
  - bring your nopcommerce application from dockerhub
create a basic template for deployment of nopcommerce.

```yaml
---
apiVersion: v1
kind: Deployment
metadata:
  name: nop-deployment
  labels:
    app: nop
    purpose: deployment
spec:
  minReadySeconds: 5
  replicas: 3
  selector:
    matchLabels:
      app: nop
  strategy:
    type: RollingUpdate # "0-downtime"
    rollingUpdate:
      maxSurge: 50%
      maxUnavailable: 25%
  template:
    metadata:
      labels:
        app: nop
        version: v1.1
    spec:
      containers:
        - name: nopCommerce
          image: dockertiru/nopcommerce2309
          ports:
            - containerPort: 80
              protocol: TCP   
```

  Recreate ---> Down time approch (bring down recreate)
  RollingUpdate ---> 0-downtime

we can try to without ec2 server...
[create cluster....and apply]
  ^ kubectl apply -f <floder Name>
  ^ kubectl get deploy,rs,po
  ^ kubectl get all

## Create 3 differnt pages with 3 diff colours....    ----> RT (02:21:00)

- Create one ec2 and install docker...
<!-- "Advanced details"
  #!/bin/bash
  cd /tmp
  curl -fsSL https://get.docker.com -o install-docker.sh
  sh /tmp/install-docker.sh
# -->

- Adding Custom HTML `/user/share/nginx/html`
  web:-> index.html in nginx docker image
  web-> html background colour

- Create Docekr instance
  ^ docker container run -d -P nginx
  ^ docker container exec awesome_tharp /bin/bash
inside the container
  ^ /user/share/nginx/html/
  ^ ls
  ^ cat index.html
  
- login ec2 now `docker`
  ^ docker info
  ^ sudo usermod -aG docker ubuntu
  ^ exit & relogin
  ^ mkdir deploy-sample
  ^ cd deploy-sample

- Create a Repository in Docker Hub.. `deploy-sample`
==x==
- in vs code
    log in the deploy-sample and create...
  - dockerfile
  - index.html

Dockerfile

```bash
FROM nginx:latest
COPY index.html /user/share/nginx/html/index.html
```

index.html

```bash
<!DOCTYPE html>
<html>
<body style="background-color:orange;">

<h1>version v2.0</h1>


</body>
</html>

```

        ==x==
  ^ cd deploy-sample
  ^ docker login
 Username:
 Password:*******
 ^ vi Dockerfile

Dockerfile

```bash
FROM nginx:latest
COPY index.html /user/share/nginx/html/index.html
```

- Docker Image build
  ^ docker image build -t <docker-repository name:v1.0 .>
  ^ docker container run -d -P --name version1 <docker-repository name:v1.0>
  ^ docker container ls
web:-> <ec2 public IP:port number of container>
[orange colour is showing now.....]

- push that image into docker hub...
  ^ docker image push <dockerhub repository name/deploy-smple:v1.0>

          ===xxxx===

- Index.html
  ^ vi index.html

```bash
<!DOCTYPE html>
<html>
<body style="background-color:green;">

<h1>version v2.0</h1>


</body>
</html>

```

  ^ docker image build -t <dockerhub repository name/deploy-smple:v2.0 .>
  ^ docker container run -d --P --name version2 <dockerhub repository name/deploy-smple:v2.0>
web:-> <ec2 public IP:port number of container>
[green colour is showing now.....]

  ^ docker image push <dockerhub repository name/deploy-smple:v2.0>

         ===xxxx===

- Index.html
  ^ vi index.html

```bash
<!DOCTYPE html>
<html>
<body style="background-color:yellow;">

<h1>version v2.0</h1>


</body>
</html>

```

  ^ docker image build -t <dockerhub repository name/deploy-smple:v3.0 .>
  ^ docker container run -d --P --name version2 <dockerhub repository name/deploy-smple:v3.0>
web:-> <ec2 public IP:port number of container>
[green colour is showing now.....]

  ^ docker image push <dockerhub repository name/deploy-smple:v3.0>

          ===xx===

## Performing Rolling updates and Rollback using Deployments --->RT (02:36:00)

- Lets create a k8s manifest to deploy an application:-
  - we need to docker hub repogitory with 3 tag colour....
  -

- Create with 10 replicas and service exposed via loadbalancer
  - create folder `depoly`--> file1 `ds-deploy.yaml`/ file2 `ds-svc.yaml`

`ds-deploy.yaml` - deploysample-deploy.yaml

```bash
---
apiVersion: v1
kind: Namespace
metadata:
  # name: prod

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ds-deploy
  # namespace: prod
spec:
  minReadySeconds: 1
  replicas: 10
  selector:
    matchLabels:
      app: web
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 30%
      maxUnavailable: 20%
  template:
    metadata:
      labels:
        # app: web
    spec:
      containers:
        - name: deploysample
          image: shaikkhajaibrahim/deploy-sample:v1.0
          ports:
            - name: webport
              containerPort: 80
              protocol: TCP
```

deploysample-service.yaml - `ds-svc.yaml`

```bash
---
apiVersion: v1
kind: Service
metadata:
  name: web-svc
  # namespace: prod
spec:
  type: LoadBalancer
  selector:
    # app: web
  ports:
    - name: websvcport
      targetPort: webport 
      port: 80
```

- add `tap` --> kubectl set namespace  
  ^ `kubectl config set-context --current --namespace=prod`

- Create deploy..>
  ^ kubectl apply -f .\ds-deploy.yaml
  ^ kubectl get deploy -n prod
  ^ kubectl get deploy,rs,pod

<!-- add to git 
  ^ git add . commit push ----> 3 -->

- Create services...>
  ^ kubectl apply -f .\ds-svc.yaml
  ^  kubectl get svc
  ^ kubectl get svc -w
      - here the EXTERNAL-IP COPY
- Access the application
  - web:-> external-ip:80

-
  ^ kubectl roolout status deployment/de-deploy
  ^ kubectl rollout history deployment/ds-deploy
REVISION    CHANGE-CASE
  1           <none>
  
# Annotation:     ---> RT (03:03:00)

- it's like LABLES...
- We will be adding an annotation to add
   `change cause` `kubernetes.io/change-cause`
- its create internal load balncer (K8s dose not create internal load balencer...)

In ds-deploy.yaml

```bash
apiVersion:
kind:
metadata:
  name: ds-deploy
  # namespace: prod
  annotations:
    kubernetes.io/change-cause: "image updated to v2.0"
.
.
.
.
# change the spec:-
    spec:
      containers:
        - name: deploysample
          image: shaikkhajaibrahim/deploy-sample:v2.0 
          ports:
            - name: webport
              containerPort: 80
              protocol: TCP
```

  ^ kubectl get svc
take the EXTERNAL-IP and web:-> *****:80

- add to git--> git add, commit, push

  ^ kubectl apply -f ./ds-deploy.yaml
  ^ kubectl rollout status deployments/ds-deploy
change the colour

  ^ kubectl rollout history deployments/ds-deploy
image update to v2.0

- Lets rollback to revision 1
  [rolling back a deployment]
  - Rolling back to a previous revision
  ^ kubectl rollout undo deployments/ds-deploy --to-revision=1
  ^ kubectl rollout status deployments/ds-deploy
....
....
.....
.....
change the old version...
  [please update `change-cause`]

  ^ kubectl rollout history deployments/ds-deploy
  ^ kubectl rollout undo deployments/ds-deploy --to-revision=2
  ^ kubectl rollout status deployments/ds-deploy
................>>>>

  ^ kubectl delete -f .\deploy\
delete deploy folder....>>>>>>>>>>

  ^ kubectl config set-context --current --namespace=default

    `==xxxx==`

## Health Checks in Kubernetes:     ----> RT (03:20:00)

...?

==================================================================

## 17/09/23

-----------
[https://directdevops.blog/2023/09/17/devops-classroomnotes-17-sep-2023/]

### ConfigMaps and Secrets

# ConfigMap

[https://kubernetes.io/docs/concepts/configuration/configmap/]

- A ConfigMap is an API object used to store non-confidential data in key-value pairs.
- They are used to store non-credintal information (the information data was not sensitive) and make it availabel to contaIner in pods.

- Configuration files (command line arg)
- urls (http://.....)
- debug (debug: information)
- mysql_host (mysql_host:services)

        1. ENV (Environmental variables)
        2. Volume mounted to some folder
              - urls, debug, mysql_host

# Secrets

[https://kubernetes.io/docs/concepts/configuration/secret/]

- store sensitive information.
- A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key.
- difference is values in secrets should be base64 encode
[https://www.base64encode.org/]
- Create a simple pod spec which mounts
    username from config map
    password from secret

  - Create one folder `configmapsandsecrets`---> in that folder
    - config.yaml
    - secret.yaml
    - pod.yaml
    - volume.yaml (podwithvol.yaml)

# config.yaml

```bash
---
apiVersion: v1
kind: ConfigMap
metadata:
  # name: userinfo-cm
data:
  username: qtdevops
```

# secret.yaml

```bash
---
apiVersion: v1
kind: Secret
metadata:
  # name: userinfo-secret
data:
  password: cXRkZXZvcHNAMTIz
            # in gitbash (create a password)
            # echo -n 'qtdevops@123' | base64
            < cXRkZXZvcHNAMTIz- this is the password >
```

# pod.yaml

```bash
---
apiVersion: v1
kind: Pod
metadata:
  name: cm-s-demo
  labels:
    app: demo
spec:
  containers:
    - name: exp
      image: alpine
      # command:
        - sleep
        - 1d
      envFrom:
        - configMapRef:
            # name: userinfo-cm
        - secretRef:
            # name: userinfo-secret
```

  ^ save to `git` and pull

  ^ kubectl apply -f ./configmapsandsecrets\
  ^ kubectl exec -it cm-s-demo -- /bin/sh (# alpine)
detaile about username, password....>>

all the done ...> push to github....>>
bash:- echo
sh:- printenv
===============

# create a volume

podwithvol.yaml

```bash
---
apiVersion: v1
kind: Pod
metadata:
  name: cm-s-demo-2
  labels:
    app: demo
spec:
  containers:
    - name: exp
      image: alpine
      command:
        - sleep
        - 1d
      # volumeMounts:
        - name: username-vol
          mountPath: /creds/username
        - name: password-vol
          mountPath: /creds/password
  # volumes:
    - name: username-vol
      configMap:
        name: userinfo-cm
    - name: password-vol
      secret:
        secretName: userinfo-secret
```

  ^ kubectl apply -f .\contigmapsandsecrets\
  ^ kubectl exec -it cm-s-demo-2 -- /bin/sh
  ^ ls /creds/
  ^ cat /creds/username/username
  ^ cat /creds/password/password
add to git....>>>

  ^ kubectl delete -f .\configmapsandsecrets\

    `==xxxx==`
  
# Excersis

- Create a docker container with mysql where you set
    username
    password
    rootpassword
    database name

Ans:-
  we need ENVIRONMENTAL VARIABLES
web:-> [https://hub.docker.com/_/mysql]
    - MYSQL_ROOT_PASSWORD
    - MYSQL_DATABASE
    - MYSQL_USER
    - MYSQL_PASSWORD
  
now create docker play ground vm and apply the command

    ^ docker run -d \
      --name mysql-container \
      -e MYSQL_ROOT_PASSWORD=myrootpassword \
      -e MYSQL_USER=myuser \
      -e MYSQL_PASSWORD=mypassword \
      -e MYSQL_DATABASE=mydatabase \
      mysql:latest

   `==xxxx==`

## Database for nop
  Create a folder `database`--->
        - mysql-secrets.yaml
        - mysql-pod.yaml

# mysql-secrets.yaml

```bash
---
apiVersion: v1
kind: Secret
metadeta:
  # name: db-cred
data:
  MYSQL_ROOT_PASSWORD: qtdevops1234  [`# use base64 to secret`]
  MYSQL_DATABASE: nop          [`# use base64 to secret`]
  MYSQL_USER: nop              [`# use base64 to secret`]
  MYSQL_PASSWORD: qtdevops123  [`# use base64 to secret`]
                          --> in git bash
                        ^ echo -n 'qtdevops123' | base64
```

# mysql-pod.yaml

```bash
---
apiversion: v1
kind: Pod
metadata:
  name: nopdb
  labels:
    app: nopdb
spec:
  containers:
    - name: nopdb
      image: mysql:8
      envFrom: 
        - secretRef:
            # name: db-cred
    
```

  ^ kubectl apply -f .\database\
  ^ kubectl exec -it nopdb -- mysql -u nop -p
enter passed: ***** [qtdevops123]

  ^ show databases;
  ^ use nop;
  ^ exit
puss to git...>>>>

all done delete database
  ^ kubectl delete database

### Kubernetes volumes:      -----> RT (01:06:00)

[https://kubernetes.io/docs/concepts/storage/volumes/]
    - provide persistent storage to pods.
    - share and store data that survives the lifetime of a pod.

- Types of Volumes
    1. Volumes: These are ephemeral (temporary)
      - store and share data between containers within a pod.
    2. PersistentVolumes (PVs):
      - PVs are suitable for ephemeral data storage within a pod, they are not designed for long-term data persistence or data sharing across pods.
        [https://kubernetes.io/docs/concepts/storage/persistent-volumes/]

# Kubernetes Storage Classes:-

[https://kubernetes.io/docs/concepts/storage/storage-classes/]

- Familiarity with volumes and persistent volumes is suggested.
- it can be use to
      volumes or persistent volumes...

              `01:11:00`

### Elastic Kubernetes Service (EKS)   ----> RT (01:47:00)

- configure aws cli
      create IAM user
        give permitions of administratiraccess
          give security credentials
            access kuys (add )

- This is managed service from AWS
- EKS is easily created from a tool called as eksctl

- Install aws cli and configure authentication for aws iam user
  - Lets create a config file ekscluster.yaml

  - install AWS cli
  ^ choco install cli....

  - Install EKS
  [https://eksctl.io/installation/#for-windows_1]
  ^ choco install eksctl
  ^ aws --version

## Lens       ------------>RT (01:51:00)

- no need to install right now..
- install Lens
  [https://k8slens.dev/]
  - connect kubectl to kubernetes cluster...
  
- Create a config folder `eks` inside --->`ekscluster.yaml`
[https://eksctl.io/usage/creating-and-managing-clusters/]
ekscluster.yaml:-

```yml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: qteks-cluster
  region: ap-south-1

nodeGroups:
  - name: ng-1
    instanceType: t2.large
    
    desiredCapacity: 2
```

  ^ eksctl create cluster -f .\ekscluster.yaml
  ^ kubectl get nods
ip-192-168-24-157.ec2.internal   Ready    <none>   4m11s   v1.27.5-eks-43840fb
ip-192-168-62-107.ec2.internal   Ready    <none>   4m11s   v1.27.5-eks-43840fb
  ^ kubectl get sc

You Create `eksctl` -----> eksctl can create
                `cloud formation` -----> cf can create
                        `kubernetes cluster`

## Storage Class    ----> RT (02:34:00)

  create `Datebase` folder -->
        - mysql-pvc.yaml ()
        - mysql-sc.yaml  (storage class)

`mysql-sc.yaml` --> storage class

```bash
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-sc
provisioner: ebs.csi.aws.com
volumeBindingMode: WaitForFirstConsumer
```

`mysql-pvc.yaml` -->
```bash
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nopdb-pvc
spec:
  accessModes: 
    - ReadWriteOnce
  storageClassName: nop-retain
  resources:
    requests:
      storage: 5Gi
```

    02:39:00

==================================================================

# 24/09/23

----------
[https://directdevops.blog/2019/11/02/deploying-the-docker-application-and-mysql-with-volume-support-into-kubernetes-from-code-to-docker-registries-like-acr-ecr-and-then-to-eks-aks/]

### helm

security group
---------------

attach surgace
attace

red team
blue team

varacode
CVA
OWASP top 10

hardning
    system hardning
    sofware hard

kube bench

SCA
Software composition analysis - sonarqube
x-ray - jforg

- vulnerability management

<!-- 
am i auduble - people on the web..
Ooook...
Baaboii...
Siggulekunda copy cheseddham...
image ha bokka...
edho okati veseddhm...
chiii...
seriously...
-->