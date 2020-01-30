### Objective

This Lab will help you to store caller information on persistent disk and return it.

### Relevant Material

[Tutorial](https://learning.cloudplex.io/cloudplex-labs/docs/Tutorial5)

[Video]()

### Code Repository

https://github.com/cloudplex-io/callerinfo-sample-app

### Cloud Provider

CloudPlex platform gives you the freedom of choosing you any cloud provider among these four (AWS, AZURE, GCP and DO). Please select any of them to proceed.

### Cloud Profile Credentials

You have to provide your selected cloud credentials in order to further continue this lab. There are fields under each cloud provider tab, fill them out.

Click on **next** button in top right corner.


### Add Volume Service

A [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) (PV) is a piece of storage in the cluster that has been dynamically provisioned by Kubernetes using a [Storage Class](https://kubernetes.io/docs/concepts/storage/storage-classes).

Hostfet application requires persistent volume to store **caller** information.

Lets drop a volume service on canvas which will create **Storage Class**, **Persistent Volume Claim**, and **Persistent Volume** 

Locate the **Volume** service in the palette.

![Lab03-add-volume-service-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-01.png)

Drag volume service from palette and drop it on canvas

![Lab03-add-volume-service-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-02.png)

Type namespace **default** of the service

![Lab03-add-volume-service-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-03.png)

Select Volume type **gp2** of the service

![Lab03-add-volume-service-04](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-04.png)

Type volume size **1** in the size text field

![Lab03-add-volume-service-05](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-05.png)

Click on the save button to save the configuration of the service

![Lab03-add-volume-service-06](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-06.png)

### Add hostfet Service

Hostfet application is a restful microservice which stores **caller** information on the volume

Locate the **Container** service in the palette.

![Lab03-add-volume-service-07](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-07.png)

Drag **container** service from palette and drop it on canvas

![Lab03-add-volume-service-08](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-add-volume-service-08.png)

#### Create Dependency

Click on the volume service and locate an arrow below it, then drag this arrow towards container service

![Lab03-create-dependency-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-create-dependency-01.gif)



Select the service to open configuration of the service on the right side of the window

![Lab03-contianer-serivce-configuraion-01]https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-01.png)

1. Change name of the service to **hostfet**

   ![Lab03-contianer-serivce-configuraion-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-02.png)

2. Enter the image name **cloudplexng/hostfet**

   ![Lab03-contianer-serivce-configuraion-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-03.png)

3. Enter tag of the image **v1**

   ![Lab03-contianer-serivce-configuraion-04](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-04.png)

4. Click on the download button to fetch metadata of the service

**Mount Volume**

All the volume will be available in **container service** which have dependency between them. 

Lets select the volume which we have added on the canvas and provide the mount path

Click on Advanced Configurations your then select Configure Volume Containers section.

![Lab03-contianer-serivce-configuraion-05](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-05.png)

Select your volume and type mount path

![Lab03-contianer-serivce-configuraion-06](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-06.png)

Click on the back button on top of the configurations.



#### Add new Environment Variable

They are required to  expose information to containers running in the Pod. Click on the **Environment variables section** to add a new [environment variable](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

![Lab03-contianer-serivce-configuraion-07](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-07.png)



CloudPlex provides two types of variables (**Static, Dynamic**). Let's add a static environment variable.

```yaml
Key : DIR_PATH
Value : /caller-data
```
** **/caller-data** is the volume mount path


![Lab03-contianer-serivce-configuraion-08](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-08.png)

Click on the back button on top of the configurations.

#### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Lab03-contianer-serivce-configuraion-09](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-09.png)

Click on Add ports button to add a new port

```yaml
name : http-3550
container Port : 3550
```

![Lab03-contianer-serivce-configuraion-10](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-10.png)

Click on the back button on top of the configurations.

![lab02-configure-service-21](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-21.png)

### Enable Ingress Traffic

​	[Ingress gateway](https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/) will allow you to access service from the internet. Click on the Ingress section to enable ingress traffic.

![Lab03-contianer-serivce-configuraion-11](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-contianer-serivce-configuraion-11.png)

Click on the back button on top of the configurations.

#### Save Service

Click on the save button to save the configuration of the service

### Save Application

Click on the **Save** button at the bottom right corner

![Lab03-application-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-application-01.png)



### Your Application Logs

In the log window, you can see the logs of your infrastructure, Kubernetes Cluster and Application which you have deployed.

**!! Deployment will take around 15 minutes!!** 

![Lab03-Deployment-Logs-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-Deployment-Logs-01.png)



### Accessing Your Application

Click on the App to get Ingress gateway Endpoint

![Lab03-Ingress-Endpoint-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/persistent%20volumes/labs/hostfet/images/Lab03-Ingress-Endpoint-01.png)



Copy Ingress Endpoint and Paste in browser new Tab. 



### Cleanup

Click on the **Terminate** button to remove all the resources from the cloud.
