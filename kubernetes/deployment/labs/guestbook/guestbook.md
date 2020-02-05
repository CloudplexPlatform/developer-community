### Objective

This Lab will help you to deploy Redis and Guestbook application.

### Relevant Material

[Tutorial](https://learning.cloudplex.io/learning/docs/guestbook-tutorial)

[Video]()

### Code Repository

​	https://github.com/kubernetes/examples/tree/master/guestbook

### Cloud Provider

CloudPlex platform gives you the freedom of choosing you any cloud provider among these four (AWS, AZURE, GCP and DO). Please select any of them to proceed.

### Cloud Profile Credentials

You have to provide your selected cloud credentials in order to further continue this lab. There are fields under each cloud provider tab, fill them out.

Click on **next** button in top right corner.

### Docker Registry

​	gcr.io/google-samples/gb-frontend

​	k8s.gcr.io/redis

### Add Service

CloudPlex has integrated with [Cloud Provider registries](https://hub.docker.com/) which allows users to access prebuilt images. You can fetch images metadata (Environment variables, Ports).

Drag **Container** service from palette and drop it on canvas. 

![container](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/container.gif)

### Configure Redis Master Service 

Select the service to open configuration of the service on the right side of the window

![lab02-configure-service-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-01.png)

1. Change name of the service to **redis-master**

   ![Service configuration 02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-02.png)

2. Enter the image name **k8s.gcr.io/redis**

   ![lab02-configure-service-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-03.png)

3. Enter tag of the image **e2e**

   ![lab02-configure-service-04](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-04.png)


#### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![lab02-configure-service-05](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-05.png)



Click on Add ports button to add a new port

![lab02-configure-service-06](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-06.png)

```yaml
name : http-6379
container Port : 6379
```

![lab02-configure-service-07](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-07.png)

Click on the back button on top of the configurations.

![lab02-configure-service-08](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-08.png)

#### Save Service

Click on the save button to save the configuration of the service

![lab02-configure-service-09](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-09.png)

### Configure Redis Slave Service

Drag another **Container** service from palette and drop it on canvas. 

![container-service](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/container-service.gif)

Select the service to open configuration of the service on the right side of the window

![lab02-configure-service-10](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-10.png)

1. Change name of the service to **redis-slave**

   ![lab02-configure-service-11](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-11.png)

2. Enter the image name **gcr.io/google_samples/gb-redisslave**

   ![lab02-configure-service-12](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-12.png)

3. Enter tag of the image **v3**

   ![lab02-configure-service-13](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-13.png)


#### Add new Environment Variable

They are required to  expose information to containers running in the Pod. Click on the **Environment variables section** to add a new [environment variable](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

![lab02-configure-service-14](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-14.png)



CloudPlex provides two types of variables (**Static, Dynamic**). Let's add a static environment variable.

![lab02-configure-service-15](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-15.png)

```yaml
Key : GET_HOSTS_FROM
Value : dns
```

![lab02-configure-service-16](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-16.png)

Click on the back button on top of the configurations.

![lab02-configure-service-17](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-17.png)

#### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![lab02-configure-service-18](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-18.png)

Click on Add ports button to add a new port

![lab02-configure-service-19](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-19.png)

```yaml
name : http-6379
container Port : 6379
```

![lab02-configure-service-20](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-20.png)

Click on the back button on top of the configurations.

![lab02-configure-service-21](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-21.png)

#### Save Service

Click on the save button to save the configuration of the service

![lab02-configure-service-22](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-22.png)

### Configure Frontend Service

Drag another **Container** service from palette as done in the previous steps and drop it on canvas. 

Select this service to open configuration of the service on the right side of the window

![lab02-configure-service-23](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-23.png)

1. Change name of the services to **guestbook-frontend**

   ![lab02-configure-service-24](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-24.png)

2. Enter the image name **gcr.io/google-samples/gb-frontend**

   ![lab02-configure-service-25](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-25.png)

3. Enter tag of the image **v4**

   ![lab02-configure-service-26](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-26.png)


#### Add new Environment Variable

Click on the **Environment variables section** to add a new [environment variable](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

![lab02-configure-service-27](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-27.png)



CloudPlex provides two types of variables (**Static, Dynamic**). Let's add a static environment variable.

![lab02-configure-service-28](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-28.png)

```yaml
Key : GET_HOSTS_FROM
Value : dns
```

![lab02-configure-service-29](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-29.png)

Click on the back button on top of the configurations.

![lab02-configure-service-30](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-30.png)

#### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![lab02-configure-service-31](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-31.png)

Click on Add ports button to add a new port

![lab02-configure-service-32](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-32.png)

```yaml
name : http-80
container Port : 80
```

![lab02-configure-service-33](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-33.png)

Click on the back button on top of the configurations.

![lab02-configure-service-34](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-34.png)

### Enable Ingress Traffic

​	[Ingress gateway](https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/) will allow you to access service from the internet. Click on the Ingress section to enable ingress traffic.

![lab02-configure-service-36](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-36.png)

Click on the back button on top of the configurations.

#### Save Service

Click on the save button to save the configuration of the service

![lab02-configure-service-35](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-35.png)



### Save Application

Click on the **Save** button at the bottom right corner

![lab02-configure-service-37](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-37.png)



### Your Application Logs

In the log window, you can see the logs of your infrastructure, Kubernetes Cluster and Application which you have deployed.

**!! Deployment will take around 15 minutes!!** 

![Lab02-Deployment-Logs-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/Lab02-Deployment-Logs-01.png)



### Accessing Your Application

Click on the App to get Ingress gateway Endpoint

![Lab02-Ingress-Endpoint-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/Lab02-Ingress-Endpoint-01.png)



Copy Ingress Endpoint and Paste in browser new Tab. 



#### Cleanup

Click on the Terminate button to remove all the resources from the cloud.

 ![Lab-02-cleanup-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/Lab-02-cleanup-01.png)