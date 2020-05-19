### Objective

This is Callerinfo Application Tutorial, which will help you to store caller information on persistent disk and return it.

### Overview

When working with containers, storage is typically tied to the lifecycle of the container it’s attached to. That means it’s ephemeral: when the container dies, its storage dies with it. For the most part, this is good, because it aligns with the Kubernetes philosophy of abstracting away hardware concerns.

However, it is sometimes useful to add persistent or shared storage to a container as part of a service. For example, you may want to store intermediary computation results on a disk, or read shared files from a cloud service that is exposed as a hard disk. For these use cases, Kubenetes provides storage APIs called Volumes and Persistent Volumes.

### Persistent Volumes

A persistent volume is a piece of storage available in a cluster, and is another resource the cluster manages like it does the compute resources in the nodes. The simplest way to create a persistent volume is statically, that is, you allocate the volume independently and then tell Kubernetes to take over. 

For example, if you host your cluster on AZURE, you might create an AZURE Disk and assign it to the cluster. To do so, you simply spin up the disk in AZURE, grab the resource handle, and then put it in the config spec as a volume.

More commonly, Kubenetes also allows you to create Persistent Volumes dynamically, that is, you can configure the cluster to scale storage up and down as needed. To do this, you need two additional components: a storage class and a claim.


### Storage Class

A storage class is like a recipe for how to create storage, or a class definition in programming. It tells the Kubernetes cluster how to provision storage and what type of storage to provision. To define a class, you need to supply a few pieces of data.

The provisioner tells the cluster where to acquire storage. You can specify cloud providers, like AWS or vSphere, or you can specify hardware storage like NFS or local. 

The reclaimPolicy tells the cluster what to do after the storage is no longer needed. You can either specify to delete the volume or retain it in for future reuse.

On top of these, there are additional parameters related to platform or implementation-specific features. These allow you to specify, for example, which Availability Zone your volumes are created in to prevent you from creating all your cloud resources in the same data center.

A sample storage class for generating small, persistent AWS volumes might look like this:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Delete
allowVolumeExpansion: false
volumeBindingMode: Immediate


```

### Persistent Volume Claims

Following the programming metaphor, once you’ve defined the class it’s time to focus on implementation. A Persistent Volume Claim is a request to instantiate storage resources defined in your storage class, and associate them with a service.

In a claim, we specify what we’d like to get back from our storage class. In the spec, you put the storage class name, as well as the size of storage you’d like and the access mode you’d like. Here, we show a request for a 5 GB volume of the class we defined above, where we have Read &Write access.


```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: exampleclaim
spec:
  accessModes:
	- ReadWriteOnce
  volumeMode: Filesystem
  resources:
	requests:
  	storage: 5Gi
  storageClassName: standard
  selector:
	matchLabels:
  	release: "development"
	matchExpressions:
  	- {key: environment, operator: In, values: [dev]}

```

After making our claim the final step is to associate it with a pod. To do that, we need to add one more piece of configuration to define where and how the volume will be exposed on the pod. 

```

apiVersion: v1
kind: Pod
metadata:
  name: samplepod
spec:
  containers:
	- name: myapi
  	image: nginx
  	volumeMounts:
  	- mountPath: "/var/www/site"
    	name: samplepd
  volumes:
	- name: samplepd
  	persistentVolumeClaim:
    	claimName: sampleclaim

```

### Putting It All Together

It’s worth going over exactly what happens when we execute the above config. Kubernetes wants to deploy our pod, but sees that it has an affiliated PVC. It checks to see if it has any available storage resources that meet the claim, and decides it doesn’t. So it needs to go back to the storage class to allocate them. The storage class points to AWS’s EBS, so it makes a request to generate new storage there, attaches it to our pod, and finishes the deploy.

Likewise, when the lifecycle of this pod ends, the persistent volume’s lifecycle also needs to be resolved. If there are no other claims on the volume, we go back up the chain to the storage class and follow the retention policy. In this case, we send a request to AWS to delete the volume once it’s done.

