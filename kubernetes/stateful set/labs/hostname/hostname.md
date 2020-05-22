### Objective

This lab is to familiarize you with Kubernetes Statefulset, which will return the hostname of the running Pod.

### Code Repository

https://github.com/CloudplexPlatform/hostname-app

### Cloud Provider

CloudPlex platform gives you the freedom of choosing you any cloud provider among these four (AWS, AZURE, GCP and DO). Please select any of them to proceed.

### Cloud Profile Credentials

You have to provide your selected cloud credentials in order to further continue this lab. There are fields under each cloud provider tab, fill them out.

Click on the **next** button on the top right corner.


### Add Volume Service

A [PersistentVolume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) (PV) is a piece of storage in the cluster that has been dynamically provisioned by Kubernetes using a [StorageClass](https://kubernetes.io/docs/concepts/storage/storage-classes).

Hostname-Info application required persistent volume to store **caller** information

Lets drop a volume service on canvas which will create **Storage Class**, **Persistent Volume Claim**, and **Persistent Volume** 

Locate the **Volume** services in the pallet.

![Lab04-add-volume-service-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-01.png)

Drag volume service from palette and drop it on canvas

![Lab04-add-volume-service-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-02.png)

Type namespace **default** of the service

![Lab04-add-volume-service-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-03.png)

Select Volume type specific to your selected cloud.

![Lab04-add-volume-service-04](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-04.png)

Type volume size **1** in the size text field

![Lab04-add-volume-service-05](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-05.png)

Click on the save button to save the configuration of the service

![Lab04-add-volume-service-06](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-06.png)

### Add hostname-info Service

Hostname-Info application is a restful microservice which will return Hostname information

Locate the **Container** services from K8 resources in the pallet.

![Lab04-add-volume-service-07](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-07.png)

Drag-n-drop **container** service from pallet to canvas

![Lab04-add-volume-service-08](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-add-volume-service-08.png)

Select the service to open configuration of the service on the right side of the window

![Lab04-contianer-serivce-configuraion-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-contianer-serivce-configuraion-01.png)

1. Change name of the service to **hostname-info**

   ![Lab04-contianer-serivce-configuraion-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-container-service-configuration-02.png)

2. Select **Statefulset** from the type dropdown

   [Statefulset](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) is the workload API object used to manage stateful applications.

   ![Lab04-container-service-configuration-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-container-service-configuration-03.png)

3. Enter the image name **cloudplexng/hostname-info**

   ![Lab04-container-service-configuration-05](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-container-service-configuration-05.png)

4. Increase the number of replicas to **2**

   ![Lab04-container-service-configuration-06](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-container-service-configuration-06.png)

5. Enter tag of the image **v1**

   ![Lab04-container-service-configuration-04](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-container-service-configuration-04.png)


**Mount Volume**

All the volume will be available in **container service** which have dependency between them. 

Lets select the volume which we have added on the canvas and provide the mount path

Click on Advanced Configurations then select Configure Volume Containers section.

![Lab04-advanced-configuration-button](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-advanced-configuration-button.png)

Click on **Add Volume** then select your volume and provide mount path.
**"/caller-data"** is the volume mount path.

![Lab04-contianer-serivce-configuraion-06](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-contianer-serivce-configuraion-06.png)

Click on the back button on top of the configurations.



### Add new Environment Variable

Click on the **Environment variables section** to add a new [environment variable](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

![Lab04-contianer-serivce-configuraion-07](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-contianer-serivce-configuraion-07.png)



Cloudplex provides two types of variables (**Static, Dynamic**). Let's add a static environment variable.

```yaml
Key : DIR_PATH
Value : /caller-data
```


![Lab04-contianer-serivce-configuraion-08](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-contianer-serivce-configuraion-08.png)

Click on the back button on top of the configurations.

### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Lab04-contianer-serivce-configuraion-09](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-contianer-serivce-configuraion-09.png)

Click on Add ports button to add a new port

```yaml
name : http-3550
container Port : 3550
```

![Lab04-contianer-serivce-configuraion-10](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-contianer-serivce-configuraion-10.png)

Click on the back button on top of the configurations

![Lab04-back-button](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-back-button.png)


### Enable Ingress Traffic

​[Ingress gateway](https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/) will allow you to access service from the internet. Click on the Ingress section to enable ingress traffic.

![Lab04-contianer-serivce-configuraion-11](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-contianer-serivce-configuraion-11.png)

Click on the back button on top of the configurations.

#### Save Service

Click on the save button to save the configuration of the service

### Save Application

Click on the **Save** button at the top right corner

![Lab04-application-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-application-01.png)



### Your Application Logs

In the log window, you can see the logs of your infrastructure, Kubernetes Cluster and Application which you have deployed.

**!! Deployment will take around 15 minutes!!** 

![Lab04-Deployment-Logs-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-Deployment-Logs-01.png)



### Accessing Your Application

Click on the App to get Ingress gateway Endpoint

![Lab04-Ingress-Endpoint-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab04-Ingress-Endpoint-01.png)


Copy ```<Ingress Endpoint>/hostname``` and Paste in browser new Tab.

### Expected Result

You will get this screen by copying that ingress Endpoint in your browser

![Lab05-browser-output-1](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab05-browser-output-1.png)

Now hit that link one more time in your browser.

![Lab05-browser-output-2](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/stateful%20set/labs/hostname/images/Lab05-browser-output-2.png)


### Cleanup

Click on the **Terminate** button to remove all the resources from the cloud.
