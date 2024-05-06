**Resource sharing**

Kubernetes cluster can be in dev/staging/prod environment. How do you allocate resources of cluster to multiple teams.
As a devops engineer how do you allocate resources . 32 /64 gb ram for one workernode 
Crashloopbackoff oom killed-> memory resource crunch. Cuz pod in one namespace login are consuming more memory, so pod in another namespace transaction are throwing crashloopback oom error.

So solution is you assign **Resource Quota** limit to **namespace**. All the services within that namespace will not occupy resource more than their limit.

When you approach dev team or any namespace they will do performance benchmarking and let you know how much is their requirements of resources and then allocate them resource quota. 
To increase this resource quota you can increase worker node count and set resource quota at namespace level.
So blast radius is reduced as service that is causing memory crunch will not effect the entire cluster but only that specific namespace.
Another 50% is solved by setting **resource limit** at pod level. So performance benchmarking is done of every microservice by dev team. You will take details you will set resource limits. 
If any microservice is causing memory leak, it's blast radius is reduced further pod level.


**Cluster upgrade**

Our cluster is kubeadm or eks 

We have prepared manual with detailed steps. 

Steps like _ how to take backup , go through release notes(whenever there is new version, it's important to read release notes, any feature is depricated might affect our cluster etc.)

I have divided steps for controlplane(etcd,api,scheduler) and worker node components. 

First you cordon(make unscheduleable) and then drain the nodes. 

Disconnect node, upgrade the kubelet of  node and join it back to Kubernetes cluster by uncordon it.   

Do this one node at a time. This will populate back pods on that node.
