### Objective

This Lab will help you to run a simple HelloWorld Application from CloudPlex.

### Relevant Material

[Tutorial]()

[Video]()

### Code Repository

​	https://github.com/cloudplex-io/hello-world

### Cloud Provider

CloudPlex platform gives you the freedom of choosing you any cloud provider among these four (AWS, AZURE, GCP and DO). Please select any of them to proceed.

### Cloud Profile Credentials

You have to provide your selected cloud credentials in order to further continue this lab. There are fields under each cloud provider tab, fill them out.

Click on **next** button on top right corner.

### Add Service

CloudPlex has integrated with [Docker Hub](https://hub.docker.com/) registry which allows users to access prebuilt images. You can fetch images metadata (Environment variables, Ports).

Drag **Docker Hub** service from palette and drop it on canvas. 

![ezgif.com-video-to-gif](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/ezgif.com-video-to-gif.gif)



### Search Hello World Service

Click on the service to show search panel of the service from Docker Hub. 

- Type **[cloudplexng/helloworld](https://hub.docker.com/r/cloudplexng/helloworld)**
- Select Community from the filter
- Now, click on the search button and select **helloworld** service.



![helloworld-service-dockerhub](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/helloworld-service-dockerhub.gif)



CloudPlex will select the latest version of the image. 

![Lab01-Add-Tag](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Add-Tag.png)



### Add Environment Variables

They are required to  expose information to containers running in the Pod. Click on the **Environment variables section** to add a new [environment variable](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

![Lab01-Add-EnvironmentVariable-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Add-EnvironmentVariable-01.png)



CloudPlex provides two types of variables (**Static, Dynamic**). Let's add a static environment variable.

![Lab01-Add-EnvironmentVariable-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Add-EnvironmentVariable-02.png)

```bash
Key = PORT
Value = 3000
```

![Lab01-Add-EnvironmentVariable-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Add-EnvironmentVariable-03.png)

Click on the back button on top of the configurations.

### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Lab01-Add-Ports-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Add-Ports-01.png)



```bash
Name = http-3000
Container Port = 3000
```

![Lab01-Add-Ports-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Add-Ports-02.png)

Click on the back button on top of the configurations.

### Enable Ingress Traffic

​	[Ingress gateway](https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/) will allow you to access service from the internet. Click on the Ingress section to enable ingress traffic.

![Lab01-Ingress-traffic-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Ingress-traffic-01.png)

Click on the back button on top of the configurations.

### Save Application

Click on the **Save** button at the bottom right corner

![Lab01-save-service-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-save-service-01.png)



Click on the save button to save the application

![Lab01-save-application01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-save-application01.png)



### Your Application Logs

In the log window, you can see the logs of your infrastructure, Kubernetes Cluster and Application which you have deployed.

**!! Deployment will take around 15 minutes!!** 

![Lab01-Deployment-Logs-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Deployment-Logs-01.png)



### Accessing Your Application

Click on the App to get Ingress gateway Endpoint

![Lab01-Ingress-Endpoint-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab01-Ingress-Endpoint-01.png)



Copy Ingress Endpoint and Paste in browser new Tab. 



### Cleanup

Click on the Terminate button to remove all the resources from the cloud.

 ![Lab-01-cleanup-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/pods%20and%20containers/labs/helloworld/images/Lab-01-cleanup-01.png)
